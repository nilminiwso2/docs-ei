# Monitoring WSO2 SI with Grafana

!!! tip "Before you begin:"
    To enable WSO2 Streaming Integrator to publish statistics in Grafana, follow the instructions in [Setting up Grafana to Display WSO2 SI Statistics](../admin/setting-up-grafana-dashboards.md).<br/><br/>
    To enable a Siddhi application to publish statistics to publish its statistics to Grafana, you need to specify Prometheus as the the statistics reporter via the `@App:statistics` annotation as shown below.<br/><br/>
    `@App:statistics(reporter = 'prometheus')`<br/><br/>
    For the dashboards to display statistics, at least one Siddhi application with the above configuration needs to be deployed in the Streaming Integrator Server.

## Setting Up Grafana to Monitor WSO2 Streaming Integrator

WSO2 Streaming Integrator performs streaming operations via Siddhi applications, which are applications written in the [Siddhi Query Language](https://siddhi.io/en/v5.1/docs/). 

Each Siddhi application contains a combination ofSiddhi components.

For the purpose of monitoring the performance of the Siddhi components used in your WSO2 Streaming Integrator instance, it provides ten pre-configured dashboards. To view them in Grafana, follow the steps below:
 
 1. Download the following dashboards (i.e., the JSON file with the dashboard configuration) by clicking on them.
 
    - [Siddhi Overall Statistics](../examples/resources/dashboards/Siddhi%20Overall%20Statistics-1580282204141.json)
    
    - [Siddhi Server Statistics](../examples/resources/dashboards/Siddhi%20Server%20Statistics-1580282223378.json)
    
    - [Siddhi Stream Statistics](../examples/resources/dashboards/Siddhi%20Stream%20Statistics-1580282240055.json)
    
    - [Siddhi Source Statistics](../examples/resources/dashboards/Siddhi%20Source%20Statistics-1580285208526.json)
    
    - [Siddhi Sink Statistics](../examples/resources/dashboards/Siddhi%20Sink%20Statistics-1580285225995.json)
    
    - [Siddhi Query Statistics](../examples/resources/dashboards/Siddhi%20Query%20Statistics-1580282256683.json)
    
    - [Siddhi Window Statistics](../examples/resources/dashboards/Siddhi%20Window%20Statistics-1580285269330.json)
    
    - [Siddhi Trigger Statistics](../examples/resources/dashboards/Siddhi%20Trigger%20Statistics-1580285383360.json)
    
    - [Siddhi Table Statistics](../examples/resources/dashboards/Siddhi%20Table%20Statistics-1580285249969.json)
    
    - [Siddhi Aggregation Statistics](../examples/resources/dashboards/Siddhi%20Aggregation%20Statistics-1580285366634.json)
    
    - [Siddhi On Demand Query Statistics](../examples/resources/dashboards/Siddhi%20On-Demand%20Query%20Statistics-1580285396455.json)
    
 2. Start and access Grafana. Then import the eleven dashboards you downloaded in the previous step. For more information, see [Managing Grafana Dashboards - Importing Dashboards](managing-grafana-dashboards.md#importing-dashboards).
    

 
## Accessing Grafana Dashboards for Monitoring

To navigate through the Grafana dashboards you set up for monitoring WSO2 Streaming Integrator and to analyze statistics, follow the procedure below:

1. Start Grafana and access it via `http://localhost:3000/`.

2. In the left pane, click the **Dashboards** icon, and then click **Manage** to open the **Dashboards** page. Here, you can click on the following dashboards:

    - **Siddhi Overall Statistics**
        
        This displays the overall statistics related to your Streaming Integrator instance and the Siddhi components of the Siddhi applications that are currently deployed in it.
        
        For a detailed description of the information displayed in this dashboard, see [Viewing Overall Statistics](viewing-overall-statistics.md).
    
    - **Siddhi Server Statistics**
    
        This displays statistics related to the Siddhi server. 
        
        For a detailed description of the information displayed in this dashboard, see [Viewing Server Statistics](viewing-overall-statistics.md).
    
    - **Siddhi Stream Statistics**
    
        This displays statistics related to [streams](https://siddhi.io/en/v5.1/docs/query-guide/#stream) in the Siddhi applications currently deployed in your WSO2 Streaming Integrator server
            
        For a detailed description of the information displayed in this dashboard, see [Viewing Stream Statistics](viewing-stream-statistics.md).
    
    - **Siddhi Source Statistics**
    
        This displays statistics related to [sources](https://siddhi.io/en/v5.1/docs/query-guide/#source) in the Siddhi applications currently deployed in your WSO2 Streaming Integrator server
                
        For a detailed description of the information displayed in this dashboard, see [Viewing Source Statistics](viewing-source-statistics.md).
    
    - **Siddhi Sink Statistics**
    
        This displays statistics related to [sinks](https://siddhi.io/en/v5.1/docs/query-guide/#sink) in the Siddhi applications currently deployed in your WSO2 Streaming Integrator server
                    
        For a detailed description of the information displayed in this dashboard, see [Viewing Sink Statistics](viewing-sink-statistics.md).
    
    - **Siddhi Query Statistics**
    
        This displays statistics related to [queries](https://siddhi.io/en/v5.1/docs/query-guide/#query) in the Siddhi applications currently deployed in your WSO2 Streaming Integrator server
            
        For a detailed description of the information displayed in this dashboard, see [Viewing Query Statistics](viewing-query-statistics.md).
    
    - **Siddhi Window Statistics**
    
        This displays statistics related to [windows](https://siddhi.io/en/v5.1/docs/query-guide/#named-window) in the Siddhi applications currently deployed in your WSO2 Streaming Integrator server
            
        For a detailed description of the information displayed in this dashboard, see [Viewing Window Statistics](viewing-window-statistics.md).
    
    - **Siddhi Trigger Statistics**
    
        This displays statistics related to [triggers](https://siddhi.io/en/v5.1/docs/query-guide/#trigger) in the Siddhi applications currently deployed in your WSO2 Streaming Integrator server
            
        For a detailed description of the information displayed in this dashboard, see [Viewing Trigger Statistics](viewing-trigger-statistics.md).

    - **Siddhi Table Statistics**
    
        This displays statistics related to [tables](https://siddhi.io/en/v5.1/docs/query-guide/#table) in the Siddhi applications currently deployed in your WSO2 Streaming Integrator server
            
        For a detailed description of the information displayed in this dashboard, see [Viewing Table Statistics](viewing-table-statistics.md).

    - **Siddhi Aggregation Statistics**
    
        This displays statistics related to [aggregations](https://siddhi.io/en/v5.1/docs/query-guide/#named-aggregation) in the Siddhi applications currently deployed in your WSO2 Streaming Integrator server
            
        For a detailed description of the information displayed in this dashboard, see [Viewing Aggregation Statistics](viewing-aggregation-statistics.md).
    
    - **Siddhi On Demand Query Statistics**
    
        This displays statistics related to on-demand-queries in your WSO2 Streaming Integrator server
            
        For a detailed description of the information displayed in this dashboard, see [Viewing Server Statistics](viewing-on-demand-query-statistics.md).