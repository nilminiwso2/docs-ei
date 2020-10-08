<<<<<<< HEAD
!!! note
    This section is still a work in progress and not tested.

# Observability Solutions

This section explains how to set up the observability solutions for WSO2 Enterprise Integrator.

WSO2 Enterprise Integrator offers two observability solutions referred to as the classic observability deployment and cloud native observability deployment.

If you already have an observability stack such as ELK,  or if you want more business analytics and less operational observability, it is recommended for you to use the Classic Observability Deployment. For more information about this solution, see [Classic Observability Deployment](../../administer-and-observe/using-the-analytics-dashboard.md).

If you are creating a new cloud-native deployment or if you have Prometheus, Grafana, and Jaeger as your in-house monitoring and observability tools, you can set  up and use the Cloud Native Observability Solution. For more information about this solution, see [Cloud Native Observability Solution](../../administer-and-observe/cloud-native-observability-dashboards.md).

=======
# Observe and Manage Overview

This section explains how to set up the observability solutions and perform management tasks for WSO2 Enterprise Integrator.

## Observability

Observability can be viewed as a superset of monitoring where monitoring is enriched with capabilities to perform debugging and profiling through rich context, log analysis, correlation, and tracing. Modern day observability resides on three pillars of **logs**, **metrics**, and **tracing**. Modern businesses require observability systems to self-sufficiently emit their current state(overview), generate alerts for any abnormalities detected to proactively identify failures, and to provide information to find the root causes of a system failure.

### Observability solutions

WSO2 Enterprise Integrator offers two observability solutions referred to as the cloud-native observability deployment and classic observability deployment.

<img src="../../assets/img/observability/observability-mi.png" title="Observability Solution" width="650" alt="Observability Solution"/>

The cloud-native and classic observability solution are suitable for the following combination of operations.

<table>
    <tr>
        <th>Observability solution</th>
        <th>Operations</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Kubernetes cloud-native solution</td>
        <td>
            <ul>
                <li>Metrics only</li>
                <li>Metrics + Logging</li>
                <li>Metrics + Tracing</li>
                <li>Metrics + Logging + Tracing</li>
            </ul>
        </td>
        <td>The default Kubernetes cloud-native solution comes with metrics enabled. You can also configure logging and tracing in combination with this. This solution is ideal if you want a complete cloud-native solution to observability and you already have Prometheus, Grafana, and Jaeger as your in-house monitoring and observability tools.</td>
    </tr>
    <tr>
        <td>VM cloud-native deployment</td>
        <td>
            <ul>
                <li>Metrics only</li>
                <li>Logging (add-on)</li>
                <li>Tracing (add-on)</li>
            </ul>
        </td>
        <td>The default VM cloud-native solution comes with metrics enabled. You can additionally set up logging or tracing separatly as part of this solution later. This solution is ideal if you want a complete cloud-native solution to observability, but you need to set this up on a VM. Ideally you would already have Prometheus, Grafana, and Jaeger as your in-house monitoring and observability tools.</td>
    </tr>
    <tr>
        <td>Classic deployment</td>
        <td>
            <ul>
                <li>Metrics only</li>
                <li>Tracing only</li>
                <li>Metrics and Tracing</li>
                <li>Logging separately</li>
            </ul>
        </td>
        <td>This solution uses the Analytics profile of WSO2 EI 6.x.x and if can be configured to have metrics and tracing by enabling them once set up. You will have to configure logging separately by setting it up in the Micro Integrator itself. This is useful if you require more business analytics and less operation observability and also if you already have an observability stack such as ELK.. This is a more simpler solution.</td>
    </tr>
</table>

* For instructions to set up the above observability solutions, see [Setting Up the cloud-native observability solutions](../setup/observability/setting-up-minimum-basic-observability-deployment.md) or [Setting up classic observability solution](../setup/observability/setting-up-classic-observability-deployment.md)

* For more information on how to use the cloud-native solution, see [Cloud Native Observability Solution](cloud-native-observability-dashboards.md).

* For more information on how to use the classic observability solution, see [Classic Observability Deployment](using-the-analytics-dashboard.md).

### Understanding observability solutions

WSO2 Enterprise Integrator 7.0.0 and older versions offer an analytics distribution that mainly provides business analytics functionality together with a few observability related features. Clients with comprehensive observability requirements had to rely on external tools/stacks such as ELK, Prometheus, AppDynamics, Jaeger, Zipkin, etc. This resulted in multiple scattered systems to observe the system where debugging and troubleshooting were not sufficiently stream-lined.

To address that limitation, WSO2 Enterprise Integrator 7.1.0 introduced an observability solution that utilizes a selected set of external tools together with the older analytic distribution intact. This section explains the features and usage of both solutions. 

The older analytics distribution is referred to as the Classic Observability Deployment, and the newer solution introduced with WSO2 Enterprise Integrator 7.1.0 is referred to as the Cloud Native Observability Deployment.

## Management

You can monitor and manage various artifacts that you have deployed. The following are the options that enable you to do this.

- **[Micro Integrator Dashboard](working-with-monitoring-dashboard.md)**: Allows you to perform administration tasks related to your Micro Integrator deployment
- **[Micro Integrator CLI](using-the-command-line-interface.md)**: Allows you to perform various management and administration tasks from the command line.
- **[Using the Management API](working-with-management-api.md)**: The Micro Integrator CLI and the Micro Integrator dashboard communicate with this service to obtain administrative information of the server instance and to perform various administration tasks. If you are not using the dashboard or the CLI, you can directly access the resources of the management API

## Integration with external tools

You can integrate with external tools to do the following.

**Monitoring Metrics**

- [JMX Monitoring](jmx_monitoring.md)
- [SNMP Monitoring](snmp_monitoring.md)

**TCP Message Monitoring**

- [Starting TCPMon](tcp/starting_tcp_mon.md)
- [Message Monitoring with TCPMon](tcp/message_monitoring_with_tcpmon.md)
- [Other Usages of TCPMon](tcp/other_usages_of_tcpmon.md)
>>>>>>> 1e62e069fd75a43881230556dbfa19e9065086de
