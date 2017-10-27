# OpenMessaging Specification

## License
## 0 Overview
### 0.1 What is OpenMessaging?
### 0.2 Why OpenMessaging?
### 0.3 OpenMessaging Terminologies
### 0.4 Difference between AMQP, CORBA & JMS

## 1 OMS Architecture
### 1.1 OMS Ecosystem
#### 1.1.1 Connector
##### 1.1.1.1 Source
##### 1.1.1.2 Sink
#### 1.1.2 Router
#### 1.1.3 Replicator

### 1.2 Model Components
### 1.3 Messaging Quality of Service
#### 1.3.1 Delivery Semantics
#### 1.3.2 Queue Ordering
#### 1.3.3 Durability

## 2 Model Components
### 2.1 Topic Pub/Sub
#### 2.1.1 Topic
#### 2.1.2 Publish
#### 2.1.3 Subscribe
### 2.2 Queue
## 3 Message Model
### 3.1 Message Type
#### 3.1.1 Bytes Message
#### 3.1.2 File Message
### 3.2 Message Format
#### 3.2.1 System Header
#### 3.2.2 User Header
#### 3.3.3 Message Body
### 3.3 Message System Header
#### 3.3.1 MessageId
#### 3.3.2 Topic
#### 3.3.3 Queue
#### 3.3.4 BornTimestamp
#### 3.3.5 BornHost
#### 3.3.6 StoreTimestamp
#### 3.3.7 StoreHost
#### 3.3.8 StartTime
#### 3.3.9 StopTime
#### 3.3.10 Timeout
#### 3.3.11 Priority
#### 3.3.12 Reliability
#### 3.3.13 SearchKey
#### 3.3.14 ScheduleExpression
#### 3.3.15 TraceId
#### 3.3.16 CompressionLevel
## 4 OMS Interface
### 4.1 MessagingAccessPoint
#### 4.1.1 URI Schema
### 4.2 ResourceManager
### 4.3 Producer
### 4.4 Consumer
### 4.5 Interceptor
#### 4.5.1 Producer Interceptor
#### 4.5.2 Producer Interceptor Points
#### 4.5.3 Consumer Interceptor
#### 4.5.4 Consumer Interceptor Points
### 4.6 Exception
## 5 Benchmark
## Appendix 
### Example of OpenMessaging API
### Change History

