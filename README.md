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
        "message": {
           "version":"1.0.0",
           "headers": {
               "messageId": "7F00000100002873000000000004F49C",
               "destination": "orderQueue",
               "bornTimestamp": 1533780827824,
               "bornHost": "172.24.0.101:10035",
               "compression": "gzip",
               "durability": 1,
               "extFields": {
                   "storeTimestamp": 1533780827825,
                   "storeHost": "172.24.0.102:52511",
                   "messageKey": "orderId-103368921567",
                   "correlationId": "7F00000100002873000000000004F2B4",
                   "delayTime": 30000,
                   "transactionId": "1E0578887D3F18B4AAC22B64D2B40A62",
                   "expireTime": 1533780830000,
                   "traceId": "1E0578887D3F18B4AAC22B64D2B00A5E",
                   "priority": 1
               }
            },
            "properties": {
               "service": "helloService"
            },
            "data": {}
        }
    
}
```



# Proposal
#### [specification](specification-schema.md)

# Release note

#### [Status of 1.0.0-preview Version of OpenMessaging](1.0.0-preview-release-note.md)

# Communications
Chat with us on the OpenMessaging Slack in the [#general channel:](https://openmessaging.herokuapp.com/) 
