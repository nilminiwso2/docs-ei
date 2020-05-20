# Clustered Deployment
The following sections provide information and instructions on how to deploy the Micro Integrator with a third-party load balancer.

## The deployment pattern

This deployment scenario uses a two-node Micro Integrator deployment. That is, two Micro Integrator nodes are configured to serve requests with high availability and scalability. The product nodes in the deployment are fronted by an external third-party load balancer, which routes requests to the two nodes on a round-robin basis.

<img src="../../../assets/img/clustered_deployment.png">

## Install the Micro Integrator

Let's set up two instances of the Micro Integrator.

[Download and install WSO2 Micro Integrator](../../setup/installation/install_in_vm.md). 

## Hostnames

Open the `deployment.toml` file (stored in the `<MI_HOME>/conf`) of each server instance and update the hostname.

```toml
[server]
hostname = "localhost"
```

Find more [parameters](../../../references/config-catalog/#deployment) for deployment settings.

## Cluster coordination

Most of the integration flows are stateless and don't actually require coordination when there is more than a single instance of the server running. However, the following set of artifacts requires coordination among themselves when deployed in more than a single instance of the server. 

-   Scheduled Tasks
-   Message Processors
-   Polling Inbound Endpoints
-   Event-Based Inbound Endpoints

### Database

When the nodes in the cluster need to communicate with each other, the Micro Integrator uses RDBMS-based coordination among the server nodes. That is, all the nodes communicate via a database. Hence, you need to have a database to enable coordination among the artifacts.

1.  Create a database named `WSO2_COORDINATION_DB`.

    ??? Note "Tested Databases"
        The following database types are tested with this version of the Micro Integrator:
    
        -   MySQL 8.0.19
        -   Microsoft SQL Server 2017 (RTM-CU11) (KB4462262) - 14.0.3038.14 (X64)
        -   postgres (PostgreSQL) 12.2 (Debian 12.2-2.pgdg100+1)
        -   DB2 v11.5.0.0
        -   Oracle Database 12c Enterprise Edition Release 12.2.0.1.0 - 64bit Production

2.  Open the `deployment.toml` file and update the configurations as shown below.
    
    ```toml tab='MySQL'
    [[datasource]]
    id = "WSO2_COORDINATION_DB"
    url= "jdbc:mysql://localhost:3306/clusterdb"
    username="root"
    password="root"
    driver="com.mysql.jdbc.Driver"
    pool_options.maxActive=50
    pool_options.maxWait = 60000
    pool_options.testOnBorrow = true
    ``` 

    ```toml tab='MSSQL'
    [[datasource]]
    id = "WSO2_COORDINATION_DB"
    url= "jdbc:sqlserver://<IP>:1433;databaseName=wso2greg;SendStringParametersAsUnicode=false"
    username="root"
    password="root"
    driver="com.microsoft.sqlserver.jdbc.SQLServerDriver"
    pool_options.maxActive=50
    pool_options.maxWait = 60000
    pool_options.testOnBorrow = true
    ```

    ```toml tab='Oracle'
    [[datasource]]
    id = "WSO2_COORDINATION_DB"
    url= "jdbc:oracle:thin:@SERVER_NAME:PORT/SID"
    username="root"
    password="root"
    driver="oracle.jdbc.OracleDriver"
    pool_options.maxActive=50
    pool_options.maxWait = 60000
    pool_options.testOnBorrow = true
    ```

    ```toml tab='PostgreSQL'
    [[datasource]]
    id = "WSO2_COORDINATION_DB"
    url= "jdbc:postgresql://localhost:5432/gregdb"
    username="root"
    password="root"
    driver="org.postgresql.Driver"
    pool_options.maxActive=50
    pool_options.maxWait = 60000
    pool_options.testOnBorrow = true
    ```

    ```toml tab='IBM DB'
    [[datasource]]
    id = "WSO2_COORDINATION_DB"
    url="jdbc:db2://SERVER_NAME:PORT/DB_NAME"
    username="root"
    password="root"
    driver="com.ibm.db2.jcc.DB2Driver"
    pool_options.maxActive=50
    pool_options.maxWait = 60000
    pool_options.testOnBorrow = true
    ```

### Node ID

The node ID is a unique identifier, which is used to identify the node in the cluster. This is useful in situations where certain requests need to be routed to the server node based on the node ID. For example, scheduled tasks should only run in specific nodes.

By default, a random UUID value will be used as the node ID. However, you can assign a specific node ID using the following methods:

-   System property (`nodeId`)
-   Environment variable (`nodeId`)
-   TOML configuration

    Open the `deployment.toml` file (stored in the `<EI_HOME>/conf` directory) and add the following section:

    ```toml
    [cluster_config]
    node_id = "node-1"
    ```

If the node ID is specified using multiple methods, the applicable node ID will be fetched in the given order.

### Task resolver

When you have scheduled task in your integration deployment, each task should only run in one node of the cluster. The task resolver configuration in your server nodes specifies the logic allocation of tasks to the server nodes.

-   Default resolver
    
    By default, tasks are resolved by selecting a random node from the available list of nodes in the cluster. All the tasks are resolved to the selected node. The tasks will be resolved to some other node only if the first node leaves the cluster. Optionally, you can apply the following [advanced configurations](#advanced-parameters).

    ```toml
    [task_handling]
    resolving_period = "6"
    resolving_frequency = "3"
    ```

-   Round robin resolver

    This class distributed the tasks among the nodes in a round robin fashion. In addition to that, it accepts a parameter named `task_server_count`, which specifies the number of nodes that should be present in the cluster before starting the task resolving process.

    ```toml
    [task_handling]
    resolver_class = "org.wso2.micro.integrator.ntask.coordination.task.resolver.RoundRobinResolver"
     
    [[task_resolver]]
    task_server_count = "3"
    ```

-   Task node resolver

    This class will resolve tasks to a predefined set of nodes (task nodes) in a round robin fashion. The `task_nodes` need to be defined as the `resolver_class` property.

    ```toml
    [task_handling]
    resolver_class= "org.wso2.micro.integrator.ntask.coordination.task.resolver.TaskNodeResolver"
     
    [[task_resolver]]
    task_nodes = "node-1,node-2 ,node-3,node-4"
    ```

#### Advanced parameters

The `resolving_period` and `resolving_frequency` properties are set by default as shown below. It is not recommended to change these default values.

```toml
[task_handling]
resolving_period = "6"
resolving_frequency = "3"
```

<table>
    <tr>
        <th>
            Parameter
        </th>
        <th>
            Default Value
        </th>
        <th>
            Possible Values
        </th>
        <th>
            Description
        </th>
    </tr>
    <tr>
        <td>
            <code>resolving_period</code>
        </td>
        <td>
            <code>2</code>
        </td>
        <td>
            Any integer greater than 0.
        </td>
        <td>
            The period in seconds, the leader node will resolve the unassigned tasks from the coordination database or the member nodes will schedule the tasks assigned to them.
        </td>
    </tr>
    <tr>
        <td>
            <code>resolving_frequency</code>
        </td>
        <td>
            <code>5</code>
        </td>
        <td>
            Any integer greater than 0.
        </td>
        <td>
            The frequency at which the un-assigned tasks need to be resolved by the leader node per cleaning of the invalid tasks from the coordination database.
        </td>
    </tr>
</table>

## Registry sharing

!!! Note
    Registry sharing is only required if you have Message Processors in your deployment.

Registry sharing maintains the state of the Message Processor, which is deployed in deactivated state upon new member additions. 

1.  Follow the instructions on [configuring the file-based registry](../../setup/deployment/file_based_registry.md) for a two-node deployment of the Micro Integrator.
2.  The `<MI_HOME>/registry` folder of each node in the cluster should be shared with each other. This can be done in the same way as deployment synchronization.

## Deployment synchronization

When you have a cluster of nodes, the integration artifacts deployed in each server node needs to be identical. This can be achieved by synchronizing the deployment directories of each server.

See [deployment synchronization](../../setup/deployment/deployment_synchronization.md) for instructions.

## Load balancing

If you need the HTTP/HTTPS traffic to be distributed among the nodes, you need to front them via a load balancer of your choice and balance the loads among the urls.

Follow the instructions on [setting up a load balancer](../../setup/deployment/setting_up_lb.md) for a two-node deployment of the Micro Integrator.

## Deployment hardening

Ensure that you have taken into account the respective security hardening factors (e.g., changing and encrypting the default passwords, configuring JVM security etc.) before deploying the Micro Integrator. For more information, see the [Production Deployment Checklist](../../setup/deployment/deployment_checklist.md).

## Testing the cluster

Start the server using the following standard start-up script.

* On **Linux/MacOS/CentOS** : `cd MI_HOME/bin/ sh micro-integrator.sh`
* ON **Windows** : `cd MI_HOME\bin\ micro-integrator.bat`

Upon server startup you can observe the following logs in each instance.

```bash
[2020-04-17 17:09:14,768]  INFO {RDBMSCoordinationStrategy} - Successfully joined the cluster with id [506b71d5-0ba3-4a76-8959-7fde798c56de]
```

You could observe the following member addition log in other servers when a node joins the cluster.

```bash
[2020-04-17 17:12:37,072]  INFO {ClusterCoordinator} - Member added [f5fc78fb-c147-4f66-8e5b-c0feae2b8c53]
```

You could observe the following member removal log in other servers when a node joins the cluster.

```bash
[2020-04-17 17:12:52,270]  INFO {ClusterCoordinator} - Member removed [506b71d5-0ba3-4a76-8959-7fde798c56de]
```

##  Testing task coordination

1.  Create a simple scheduled task using WSO2 Integration Studio and deploy it in the two Micro Integrator servers. See the instructions on [creating a scheduled task](../../../develop/creating-artifacts/creating-scheduled-task).

    ```toml
    <?xml version="1.0" encoding="UTF-8"?>
    <task xmlns="http://ws.apache.org/ns/synapse" name="sample-task" class="org.apache.synapse.startup.tasks.MessageInjector" group="synapse.simple.quartz">
      <trigger interval="5000"/>
      <property xmlns:task="http://www.wso2.org/products/wso2commons/tasks" name="message">
         <test xmlns="">sample-task</test>
      </property>
    </task>
    ```

2.  Observe the following log in the server.

    ```bash
    [2020-04-20 11:13:21,982]  INFO {AbstractQuartzTaskManager} - Task scheduled: [ESB_TASK][sample-task].
    ```

    The above log can be observed in only one server and this implies that the task is scheduled only in one node when coordination is enabled.

3.  Shutdown the node in which the task is scheduled and observe the following log in the other node.

    ```bash
    [2020-04-20 11:13:21,982]  INFO {AbstractQuartzTaskManager} - Task scheduled: [ESB_TASK][sample-task].
    ```

    The above log describes the failover capability of the tasks when the task server becomes unavailable.
