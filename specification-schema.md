# OpenMessaging Specification

## Table of Contents
- [License](#license)
- [Overview](#0-overview)
- [Type System](#1-type-system)
- [Message Model](#2-message-model)
- [UseCases](#openmessaging-common-usecases)
- [Appendix](#appendix)
## License
## 0 Overview
### 0.1 What is OpenMessaging?
   OpenMessaging is a cloud-native, vendor-neutral open standard for distributed messaging.
   
### 0.2 Why OpenMessaging?
#### 0.2.1 Goals
   Messaging products have been widely used in modern architecture and data processing, for decoupling, queuing, buffering, ordering, replicating, etc. But when data transfers across different messaging and streaming platforms, the compatibility problem arises, which always means much additional work. Although JMS was a good solution during the past decade, it is limited in java environment, lacks specified guidelines for load balance/fault-tolerance, administration, security, and streaming feature, which make it not good at satisfying modern cloud-native messaging and streaming applications. While OpenMessaging aims at :

   - Language-agnostic and platform independence. message standard support multiple platforms, architectures or systems.   
   - Global, cloud-native, vendor-neutral industry standard for distributed messaging.   
   - Facilitating a standard benchmark for testing applications.   
   - Targeting cloud data streaming and messaging requirements with scalability, flexibility, isolation, and security built in Fostering a growing community of contributing developers.   

#### 0.2.1 Non-Goals
   The following will not be part of the specification:   
   - Language-specific runtime APIs.     
   - Benchmark Interface for evaluating performance.       
   - Connector Interface for data stream exchange with other systems.     

### 0.3 OpenMessaging Terminologies
#### 0.3.1 Topic
   An administered object that encapsulates the identity of a message destination for messaging.
   
#### 0.3.2 Producer
   An object that sending a message to all consumers of a topic.
   
#### 0.3.3 Consumer
   An object that is used for receiving messages sent to a topic.
   
#### 0.3.4 Queue
   An administered object that encapsulates the identity of a message destination.
   
#### 0.3.5 Delivery Semantics
   When it comes to describing the semantics of a delivery mechanism, there are three  semantic guarantees between producer and consumer:   
   **At least once**: a message will be consumed at least once.  
   **At most once**: a message will be consumed at most once, in this semantics, messages may be lost.  
   **Exactly once**: a message will be consumed once and only once.  

## 1 Type System
  The following abstract data types are available for use in attributes.
  
  - `String` - Sequence of printable Unicode characters.
  - `Binary` - Sequence of bytes.
  - `KeyValue` - `String`-indexed dictionary of `String`-typed or `Binary`-typed or `Numeric`-typed values
  - `Numeric`:    
        - `Short` - Integer in the range -(2^15) to 2^15 - 1 inclusive.
        - `Integer` - Integer in the range -(2^31) to 2^31 - 1 inclusive.  
        - `Long` - Integer in the range -(2^63) to 2^63 - 1 inclusive.  
        - `Float` - A 32-bit floating point number (binary32 [IEEE754](http://ieeexplore.ieee.org/servlet/opac?punumber=4610933)).  
        - `Double` - A 64-bit floating point number (binary64 [IEEE754](http://ieeexplore.ieee.org/servlet/opac?punumber=4610933)).  
  - `Object` - Either a `String`, or a `Binary`, or a `KeyValue`, or a `Numeric`
  - `URI` - String expression conforming to `URI-reference`
    as defined in
    [RFC 3986 §4.1](https://tools.ietf.org/html/rfc3986#section-4.1).
    
  The `Object` type is a variant type that can take the shape of either a
  `String` or a `Binary` or a `KeyValue` or a `Numeric`. The type system is intentionally
  abstract, and therefore it is left to implementations how to represent the
  variant type(Reference to the `Object` description of [CloudEvents](https://github.com/cloudevents/spec/blob/v0.1/spec.md)).
 
## 2 Message Model
### 2.1 Message Type
#### 2.1.1 Bytes Message
   A message that whose body contains a stream of uninterpreted bytes. This message type is for literally encoding a body to match an existing message format.
   It will be use one of self-defining message types to encode the message body, and vendors are responsible for decode these bytes in a custom rules. 

### 2.2 Message Format
   In the OpenMessaging, a message consists of 4 parts: the version, the credential, the system header, the user header and the message body.
#### 2.2.1 version
   - Type: `String`  
   - Description: The version of OpenMessaging standard. 
   - Constraints: REQUIRED 
   
#### 2.2.2 headers
   - Type: `KeyValue`  
   - Description: All messages support the same set of header fields, and these header fields are used by system, which are usually used for such as identify and route messages.
    Specific fields can be found in the next [chapter](#2.3-message-header).
   - Constraints: REQUIRED
   
#### 2.2.3 properties
   - Type: `KeyValue`  
   - Description: In addition to the system header, OpenMessaging provides a built-in user properties for adding optional fields to a message, and these fields are represented as key-value forms.
   - Constraints: REQUIRED
   
#### 2.2.4 data
   - Type: `Binary`  
   - Description: This field is the part of transmitted data that is the actual intended message contains application data.   
   The message body is completely transparent to the server, the server cannot view or modify the message body.  
   - Constraints: OPTIONAL
   
### 2.3 Message Header
#### 2.3.1 messageId
   - Type: `String`  
   - Description: An unique identifier for a message.  When a message is sent, messageId is ignored. When the send method returns it contains a provider-assigned value.
   - Constraints: REQUIRED and MUST be a non-empty `String`.
   
#### 2.3.2 bornTimestamp
   - Type: `Long` 
   - Description: The timestamp of the message sent by the client. 
   It is not the time the message was actually transmitted because the actual send may occur later due to transactions or other client side queueing of messages.   
   When a message is sent, `bornTimestamp` is ignored. When the send method returns, the field contains a time value somewhere in the interval between the call and the return.   
   It is represented as a long value which is defined as the difference, measured in milliseconds, between this time and midnight, January 1, 1970 UTC.
   - Constraints: REQUIRED 
   
#### 2.3.3 bornHost
   - Type: `String` 
   - Description: When a message is sent, this field will be set with the local host info of client.
   - Constraints: REQUIRED and MUST be a non-empty `String`.

   
#### 2.3.4 durability
   - Type: `Integer`
   - Description: OpenMessaging defines two modes of message delivery:  
   **PERSISTENT**: when this field value is set with 0, the persistent mode instructs the vendor should provide stable storage to ensure the message won't be lost.  
   **NON_PERSISTENT**: when this field value is set with 1, this mode does not require the message be logged to stable storage, in most cases, the memory storage is enough for better performance and lower cost.  
   - Constraints: OPTIONAL
   

#### 2.3.5 compression
   - Type: `String`
   - Description: This field represents the message body compress algorithm.    
     vendors are free to choose the compression algorithm, but must ensure that the decompressed message is delivered to the user.
   - Constraints: OPTIONAL

#### 2.3.6 destination  
   -Type: `String`
   -Description: This filed contains the logic destination to which the message is being sent, such as a queue or a topic.
   When a message is sent this value is set to the right queue, then the message will be sent to the specified destination.
   When a message is received, its destination is equivalent to the queue where the message resides in.
   - Constraints: REQUIRED    
      
#### 2.3.7 extFields
   -Type: `KeyValue`
   -Description: This field contains extension metadata for message middleware, and these extension fields are not mandatory,
    but for the time being, most of the message middleware has been implemented related content more or less, and these fields have been well known 
    and understood by many messaging and streaming developers, See the [ExtFields document](./extFields.md) for a list of possible properties..

   - Constraints: OPTIONAL    
      
  
### Notational Conventions
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to
be interpreted as described in [RFC 2119](https://tools.ietf.org/html/rfc2119).

## OpenMessaging Common UseCases

This document lists the most of common use cases supported by OpenMessaging.
 
1. P2P
2. Publish/Subscribe
3. Broadcast
4. Highway
5. Streaming
6. Filter
7. Routing
8. RPC

### P2P

![](/assets/images/use_cases/15078677455707.jpg)

P2P, point to point, the simplest one, in this case, Queue is the only involved resource of OpenMessaging which only has one partition. Simply, Producer send message to Queue, and consumed by Consumer later.

### Publish/Subscribe

In this case, Producer send message to Queue with multiple partitions in Round-robin or Hash way. And these partitions will be assigned to consumers who has already subscribed the specified queue regularly.

![](/assets/images/use_cases/15078678095515.jpg)

Topic and Routing model also can be imported to this case as shown below, if necessary.

![](/assets/images/use_cases/15078678261228.jpg)

### Broadcast

![](/assets/images/use_cases/15078678568510.jpg)

In broadcast case, any message sent to the Queue will be consumed by all consumers.

### Highway

![](/assets/images/use_cases/15078678981991.jpg)

In highway case, the only focus of SequenceProducer is speed, Producer always want to send abundant and less important messages to Queue. One of the Implementation ways is Batch.

### Streaming

![](/assets/images/use_cases/15078679330640.jpg)


StreamingConsumer is for this use case, a stream-oriented consumer, to integrate messaging system with Streaming/BigData related platforms easily. StreamingConsumer supports consume messages from partitions of a specified queue like iterator.

### Filter

In most cases, original messages can’t arouse the interests of consumers, and consumers always want to consume processed messages, the most useful processing method is Filter.

As shown below, the Routing model of OpenMessaging can be applied to Filter easily. In this case, the message will be routed to Queue through two filter operators, which will keep the message with Student tag and has a property age between 18~23.

![](/assets/images/use_cases/15078679950623.jpg)

### Replication

![](/assets/images/use_cases/15078680221779.jpg)


Sometimes, the producers and consumers are distributed among multiple data centers, OpenMessaging provides a simple way to route messages from one region to another region.

### RPC

![](/assets/images/use_cases/15078681271290.jpg)

In OpenMessaging, RPC is equal to synchronous message, it isn’t traditional CS(Client2Server) model, but CSC(Client2Server2Client) model.


## Appendix 
### Example of OpenMessaging API
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

### Change History
0.3.0 version created, be compatible with existent runtime API.      
1.0.0 version created, change domain model to queue based model, add type system and schema.
