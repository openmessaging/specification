# The OpenMessaging Specification repository

This repository is a place to document (and discuss) the OpenMessaging specification itself (independent of any particular language or platform).

# Goals
OpenMessaging is vendor-neutral and language-independent, provides industry guidelines for areas of finance, e-commerce, IoT and big-data, and aimed to develop messaging and streaming applications across heterogeneous systems and platforms.

# Landscape
![landscape](assets/images/landscape-0.2.0-alpha.png)
##### MRI - OpenMessaging Runtime Interface
##### MCI - OpenMessaging Connector Interface
##### MBI - OpenMessaging Benchmark Interface

# OpenMessaging
Please see http://openmessaging.cloud/.

# Schema
```json
{
    "messages": {
        "credential": {
            "accountId": "",
            "accessKeyId": "",
        },
        "message": {
            "headers": {
                "sysHeaders": {
                   "messageId": "",
                   "bornTime": "",
                   "bornHost": "",
                   "storeTime": "",
                   "storeHost": "",
                   "deliveryMode": "",
                   "deliveryTime": "",
                   "deliveryCount": "",
                   "deliveryDelayExpression": "",
                   "ttl": "",
                   "correlationId": "",
                   "priority": "",
                   "traceId": "",
                   "transactionId": "",
                   "searchIndex": "",
                 "userHeaders": {}
            },
            "properties": {},
            "bodies": {}
        }
    }
}
```



# Proposal
#### [specification](specification.md)
#### [use case](usecase.md)


# Communications
Chat with us on the OpenMessaging Slack in the [#general channel:](https://openmessaging.herokuapp.com/) 
