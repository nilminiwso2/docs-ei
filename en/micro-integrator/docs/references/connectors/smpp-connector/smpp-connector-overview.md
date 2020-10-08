# SMPP Connector Overview

SMPP (Short Message Peer-to-Peer Protocol) is an open, industry standard protocol designed to provide a flexible data communications interface for transfer of short message data between SMSCs (Short Message Service Center). There are many SMPP gateways available in the world and now almost all the Message Centers support SMPP. 

To see the available SMPP connector, navigate to the [connector store](https://store.wso2.com/store/assets/esbconnector/list) and search for "SMPP".

<img src="../../../../assets/img/connectors/smpp-store.png" title="SMPP Connector Store" width="200" alt="SMPP Connector Store"/>

## Compatibility

| Connector version | Supported WSO2 EI version |
| ------------- |------------- |
|  1.0.3        |  EI 7.1.0, EI 7.0.x, EI 6.6.0, EI 6.5.0 |

For older versions, see the details in the connector store.

## SMPP Connector documentation

The SMPP Connector allows you to send an SMS through the WSO2 EI. It uses the [jsmpp API](https://jsmpp.org/) to communicate with an SMSC, which is used to store, forward, convert, and deliver Short Message Service (SMS) messages. JSMPP is a Java implementation of the SMPP protocol. 

* **[Setting up the SMPP Connector](smpp-connector-configuration.md)**: You need to set up the environment and SMSC simulator before using the connector.

* **[SMPP Connector Example](smpp-connector-example.md)**: This example demonstrates how to work with the WSO2 EI SMPP Connector and send SMS messages via the SMPP protocol. 

* **[SMPP Connector Reference](smpp-connector-config.md)**: This documentation provides a reference guide for SMPP.

## SMPP Inbound Endpoint documentation

The SMPP inbound endpoint allows you to consume messages from SMSC via WSO2 EI. WSO2 EI SMPP inbound endpoint acts as a message consumer. It creates a connection with the SMSC, then listens over a port to consume only SMS messages from the SMSC and injects the messages to the EI sequence. It will receive alert notifications or will notify when a data short message accepted.

* **[SMPP Inbound Endpoint Example](smpp-inbound-endpoint-example.md)**: This scenario demonstrates how the SMPP inbound endpoint works as an message consumer. 

* **[SMPP Inbound Endpoint Reference](smpp-inbound-endpoint-config.md)**: This documentation provides a reference guide for SMPP Inbound Endpoint.

## How to contribute

As an open source project, WSO2 extensions welcome contributions from the community. 

To contribute to the code for this connector, please create a pull request in the following repository. 

* [SMPP Connector GitHub repository](https://github.com/wso2-extensions/esb-connector-smpp)
* [SMPP Inbound Endpoint GitHub repository](https://github.com/wso2-extensions/esb-inbound-smpp)

Check the issue tracker for open issues that interest you. We look forward to receiving your contributions.
