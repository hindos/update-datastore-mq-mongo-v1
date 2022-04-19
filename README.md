# update-datastore-mq-mongo-v1

ACE application which updates MongoDB collection with record consumed from MQ

## Overview

This message flow GETS a JSON MQ message containing a 'customer-details' payload, and writes the contents of the message into the *customer_details* MongoDB database.

The application is designed to be used in conjunction with the create-customer-mq-soap-to-mq-json-v1 application, which takes in the SOAP request message and converts it to JSON ready for consumption by this flow.

## Message flow nodes used in the flow

The message flow is very simple, comprising of only two message flow nodes.

![update-datastore-mq-mongo-v1 overall message flow](https://github.ibm.com/cpat-agile-integration-sample/update-datastore-mq-mongo-v1/blob/master/readme.images/overall-flow.png "update-datastore-mq-mongo-v1 overall message flow")

### MQ Input

* **Queue Name:** UPDATE.DATASTORE.Q.V1
* **Policy:** CQM4 (connectivity to MQ via MQEndpoint Policy, not via the *MQ Connection* tab)
* **Input Message Parsing:** JSON

### LoopBackRequest


* **Data source name:** customer_updates
* **LoopBack object:** customer_updates
* **Operation:** Create
* **Data location:** $Body

The LoopBackRequest node utilises the connection details provided by the datasources.json file in the [ACE Config](https://github.ibm.com/cpat-agile-integration-sample/ace-configurations "datasources.json location") repository. This json file is provided to teh ACE container via a 'generic' ACE Configuration k8s object and loaded into the filesystem of the ACE container.

## Error Handling

Currently this flow does not have any error handling, but we hope to add this in future.
