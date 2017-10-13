# OpenMessaging Common UseCases

This document lists the most of common use cases supported by OpenMessaging.
 
1. P2P
2. Publish/Subscribe
3. Broadcast
4. Highway/assets/images/use_cases
5. Streaming
6. Filter
7. Routing
8. Online Test
9. Upgrade
10. RPC

## P2P

![](/assets/images/use_cases/15078677455707.jpg)

P2P, point to point, the simplest one, in this case, Queue is the only involved resource of OpenMessaging which only has one partition. Simply, Producer send message to Queue, and consumed by Consumer later.

## Publish/Subscribe

In this case, Producer send message to Queue with multiple partitions in Round-robin or Hash way. And these partitions will be assigned to consumers who has already subscribed the specified queue regularly.

![](/assets/images/use_cases/15078678095515.jpg)

Topic and Routing model also can be imported to this case as shown below, if necessary.

![](/assets/images/use_cases/15078678261228.jpg)

## Broadcast

![](/assets/images/use_cases/15078678568510.jpg)

In broadcast case, any message sent to the Queue will be consumed by all consumers.

## Highway

![](/assets/images/use_cases/15078678981991.jpg)

In highway case, the only focus of SequenceProducer is speed, Producer always want to send abundant and less important messages to Queue. One of the Implementation ways is Batch.

## Streaming

![](/assets/images/use_cases/15078679330640.jpg)


StreamingConsumer is for this use case, a stream-oriented consumer, to integrate messaging system with Streaming/BigData related platforms easily. StreamingConsumer supports consume messages from partitions of a specified queue like iterator.

## Filter

In most cases, original messages can’t arouse the interests of consumers, and consumers always want to consume processed messages, the most useful processing method is Filter.

As shown below, the Routing model of OpenMessaging can be applied to Filter easily. In this case, the message will be routed to Queue through two filter operators, which will keep the message with Student tag and has a property age between 18~23.

![](/assets/images/use_cases/15078679950623.jpg)

## Replication

![](/assets/images/use_cases/15078680221779.jpg)


Sometimes, the producers and consumers are distributed among multiple data centers, OpenMessaging provides a simple way to route messages from one region to another region.

## Online Test

![](/assets/images/use_cases/15078680617233.jpg)

Tests are important, many tests like A/B or pressure test need online environment. Create a test Queue with partial traffic can reach this goal.

## Upgrade

![](/assets/images/use_cases/15078680954998.jpg)

Image that we want to release our Consumer version 2.0, which can handle messages with tag Staff or Student, while the version 1.0 consumer only can handle messages with tag Student. OpenMessaging can cover this case easily.

## RPC

![](/assets/images/use_cases/15078681271290.jpg)

In OpenMessaging, RPC is equal to synchronous message, it isn’t traditional CS(Client2Server) model, but CSC(Client2Server2Client) model.
