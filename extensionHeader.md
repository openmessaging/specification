# OpenMessaging Extension fields
The [OpenMessaging Specification](./specification-schema.md) defines the core fields of for messaging and  
streaming, which can meet the needs of most common message middleware 
message transmissions, but there are still many fields related to the message 
domain, and are also well known to many developers, but not produced by every 
message. but not so much commonly used as the fields in OpenMessaging 
Specification, but these fields are still very meaningful and can help message 
middleware achieve more features and improve its visibility.       

So we officially defined some of the following attributes in the extensionHeader: 

## storeTimestamp
   - Type: `Long` 
   - Description: when the `durability` The timestamp that a message stored by server. when a 
   message is stored by server, this field will be set with the current 
   timestamp of server.  
   It is represented as a long value which is defined as the difference, 
   measured in milliseconds, between this time and midnight, January 1, 1970 
   UTC.       
   - Constraints: OPTIONAL 
   
## storeHost
   - Type: `String`
   - Description: The host info of the server that stores this message. when a 
   message is stored by server, this field will be set with the host info of 
   server.
   - Constraints: OPTIONAL
   
## correlationId
   - Type: `String`
   - Description: A client can use the correlationId header field to link one 
   message with another. A typical use is to link a response message with its 
   request message.
   - Constraints: OPTIONAL

## messageKey
   - Type: `String`
   - Description: This key that specifies that a message belongs to a specific 
   message group, and this key can be used for the server to shard or
     dispatch messages.
   - Constraints: OPTIONAL

## delayTime
   - Type: `Long`
   - Description: The message will be delivered after `delayTime` milliseconds 
   starting from `bornTimeStamp` .      
   When this filed isn't set explicitly, this means this message should be 
   delivered immediately.
   - Constraints: OPTIONAL
   
## expireTime
   - Type: `Long` 
   - Description: This field represents the discard time of the message, if an 
   undelivered message's `expireTime` is reached, the message would be 
   destroyed. If an earlier timestamp is set than `expireTime` or isn't set 
   , that means the message will not be expired.       
   It is represented as a long value which is defined as the difference, 
   measured in milliseconds, between this time and midnight, January 1, 1970 
   UTC.
   - Constraints: OPTIONAL
   
   
## traceId
   - Type: `String`
   - Description: This identifier represents a global and unique 
   identification, to associate key events in the whole lifecycle of a message,
   like sent by who, stored at where, and received by who. And, the messaging 
   system only plays exchange role in a distributed system in most cases,
   so the TraceID can be used to trace the whole call link with other parts in 
   the whole system.
   - Constraints: OPTIONAL

## transactionId
   - Type: `String`
   - Description: This field is used in transactional message, and it can be 
   used to trace a transaction. So the same `transactionId` will be appeared 
   not only in prepare message, but also in commit message, and consumer 
   received message also contains this field.
   - Constraints: OPTIONAL
   
## deliveryCount
   - Type: `Integer`
   - Description:  This field indicates the times of the message was 
   delivered, when a consumer consumes a message failed, it will be resend to 
   the server for consume it later. and this field records the consumed times 
   during the consume process.
   - Constraints: OPTIONAL
   
  
## priority
   - Type: `Integer`
   - Description: OpenMessaging defines a ten level priority value with 1 as 
   the lowest priority and 10 as the highest, and the default priority is 5. 
   The priority beyond this region will be ignored.      
   OpenMessaging does not require or provide any guarantee that the message 
   should be delivered  in priority order strictly, but the vendor should 
   provide a best effort to deliver expedited messages ahead of normal 
   messages.
   - Constraints: OPTIONAL
   
## partition   
   - Type: `Integer`
   - Description: This field in extension header  contains the partition of target destination which the message
   is being sent. When a Message is set with this value, this message will be delivered to specified partition, but the
   premise is that the implementation of the server side is dependent on the partition or a queue-like storage mechanism.
   - Constraints: OPTIONAL 