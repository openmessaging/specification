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
           "version":"0.3.0",
           "headers": {
               "messageId": "7F00000100002873000000000004F49C",
               "bornTimestamp": 1533780827824,
               "bornHost": "172.24.0.101:10035",
               "storeTimestamp": 1533780827825,
               "storeHost": "172.24.0.102:52511",
               "expireTime": 1533780830000,
               "priority": 1,
               "compression": "gzip",
               "traceId": "1E0578887D3F18B4AAC22B64D2B00A5E",
               "transactionId": "1E0578887D3F18B4AAC22B64D2B40A62",
               "searchKey": "hello",
               "delayTime": 30000,
               "durability": 1,
               "correlationId": "7F00000100002873000000000004F2B4"
            },
            "properties": {
               "service": "helloService"
            },
            "payload": []
        }
    }
```



# Proposal
#### [specification](specification-schema.md)


# Communications
Chat with us on the OpenMessaging Slack in the [#general channel:](https://openmessaging.herokuapp.com/) 
