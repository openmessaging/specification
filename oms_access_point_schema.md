## OMS Access Point Schema

This document describes the access point format for defining connections between applications and OpenMessaging providers.

### Standard Connection String Schema

This section describes the standard schema of the OpenMessaging access point URI used to connect to a OMS provider. The format is the same for all OMS implementation.

The following is the standard URI connection scheme:

```
oms:<driver_type>://[account_id@]host1[:port1][,host2[:port2],...[,hostN[:portN]]]/<region>
```

The components of this string are:

| Component | Description |
| --- | --- |
| oms | A required prefix to identify that this is a string in the standard OMS access point format. |
| driver_type | Required. It identifies a specific OMS provider, like RocketMQ. |
| account_id | Optional. The ID of the specific account system that owns the resource. |
| host1 | Required. It identifies a server address to connect to. It identifies either a hostname or IP address. |
| port1 | Optional. The default value is 80 if not specified. |
| hostN | Optional. You can specify as many hosts as necessary. You would specify multiple hosts. |
| portN | Optional. The default value is 80 if not specified. |
| region | Required. The target region. |

### Access Point Example

1. Single host

  The following example connects user alice to a rocketmq implementation in region us-east:

  ```
  oms:rocketmq://alice@rocketmq.apache.org/us-east
  ```

2. Multiple hosts

  The multiple hosts are often used to load balancing.

  ```
  oms:rocketmq://alice@rocketmq.apache.org, openmessaging.io/us-east
  ```
