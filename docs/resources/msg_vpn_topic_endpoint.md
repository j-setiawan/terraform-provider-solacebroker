---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "solacebroker_msg_vpn_topic_endpoint Resource - solacebroker"
subcategory: ""
description: |-
  A Topic Endpoint attracts messages published to a topic for which the Topic Endpoint has a matching topic subscription. The topic subscription for the Topic Endpoint is specified in the client request to bind a Flow to that Topic Endpoint. Queues are significantly more flexible than Topic Endpoints and are the recommended approach for most applications. The use of Topic Endpoints should be restricted to JMS applications.
  A SEMP client authorized with a minimum access scope/level of "vpn/read-only" is required to perform this operation.
  This has been available since SEMP API version 2.1.
  The import identifier for this resource is {msg_vpn_name}/{topic_endpoint_name}, where {&lt;attribute&gt;} represents the value of the attribute and it must be URL-encoded.
---

# solacebroker_msg_vpn_topic_endpoint (Resource)

A Topic Endpoint attracts messages published to a topic for which the Topic Endpoint has a matching topic subscription. The topic subscription for the Topic Endpoint is specified in the client request to bind a Flow to that Topic Endpoint. Queues are significantly more flexible than Topic Endpoints and are the recommended approach for most applications. The use of Topic Endpoints should be restricted to JMS applications.



A SEMP client authorized with a minimum access scope/level of "vpn/read-only" is required to perform this operation.

This has been available since SEMP API version 2.1.

The import identifier for this resource is `{msg_vpn_name}/{topic_endpoint_name}`, where {&lt;attribute&gt;} represents the value of the attribute and it must be URL-encoded.



<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `msg_vpn_name` (String) The name of the Message VPN.
- `topic_endpoint_name` (String) The name of the Topic Endpoint.

### Optional

- `access_type` (String) The access type for delivering messages to consumer flows bound to the Topic Endpoint. Modifying this attribute while the object (or the relevant part of the object) is administratively enabled may be service impacting as egress_enabled will be temporarily set to false to apply the change. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `"exclusive"`. The allowed values and their meaning are:

<pre>
"exclusive" - Exclusive delivery of messages to the first bound consumer flow.
"non-exclusive" - Non-exclusive delivery of messages to bound consumer flows in a round-robin fashion.
</pre>
 Available since SEMP API version 2.4.
- `consumer_ack_propagation_enabled` (Boolean) Enable or disable the propagation of consumer acknowledgments (ACKs) received on the active replication Message VPN to the standby replication Message VPN. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `true`.
- `dead_msg_queue` (String) The name of the Dead Message Queue (DMQ) used by the Topic Endpoint. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `"#DEAD_MSG_QUEUE"`. Available since SEMP API version 2.2.
- `delivery_count_enabled` (Boolean) Enable or disable the ability for client applications to query the message delivery count of messages received from the Topic Endpoint. This is a controlled availability feature. Please contact support to find out if this feature is supported for your use case. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `false`. Available since SEMP API version 2.19.
- `delivery_delay` (Number) The delay, in seconds, to apply to messages arriving on the Topic Endpoint before the messages are eligible for delivery. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `0`. Available since SEMP API version 2.22.
- `egress_enabled` (Boolean) Enable or disable the transmission of messages from the Topic Endpoint. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `false`.
- `event_bind_count_threshold` (Attributes) The thresholds for the Topic Endpoint consumer flows event, relative to `max_bind_count`. Available since SEMP API version 2.4. (see [below for nested schema](#nestedatt--event_bind_count_threshold))
- `event_reject_low_priority_msg_limit_threshold` (Attributes) The thresholds for the maximum allowed number of any priority messages queued in the Topic Endpoint event, relative to `reject_low_priority_msg_limit`. (see [below for nested schema](#nestedatt--event_reject_low_priority_msg_limit_threshold))
- `event_spool_usage_threshold` (Attributes) The thresholds for the message spool usage event of the Topic Endpoint, relative to `max_spool_usage`. (see [below for nested schema](#nestedatt--event_spool_usage_threshold))
- `ingress_enabled` (Boolean) Enable or disable the reception of messages to the Topic Endpoint. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `false`.
- `max_bind_count` (Number) The maximum number of consumer flows that can bind to the Topic Endpoint. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `1`. Available since SEMP API version 2.4.
- `max_delivered_unacked_msgs_per_flow` (Number) The maximum number of messages delivered but not acknowledged per flow for the Topic Endpoint. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `10000`.
- `max_msg_size` (Number) The maximum message size allowed in the Topic Endpoint, in bytes (B). Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `10000000`.
- `max_redelivery_count` (Number) The maximum number of times the Topic Endpoint will attempt redelivery of a message prior to it being discarded or moved to the DMQ. A value of 0 means to retry forever. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `0`.
- `max_spool_usage` (Number) The maximum message spool usage allowed by the Topic Endpoint, in megabytes (MB). A value of 0 only allows spooling of the last message received and disables quota checking. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `5000`.
- `max_ttl` (Number) The maximum time in seconds a message can stay in the Topic Endpoint when `respect_ttl_enabled` is `"true"`. A message expires when the lesser of the sender assigned time-to-live (TTL) in the message and the `max_ttl` configured for the Topic Endpoint, is exceeded. A value of 0 disables expiry. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `0`.
- `owner` (String) The Client Username that owns the Topic Endpoint and has permission equivalent to `"delete"`. Modifying this attribute while the object (or the relevant part of the object) is administratively enabled may be service impacting as egress_enabled will be temporarily set to false to apply the change. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `""`.
- `permission` (String) The permission level for all consumers of the Topic Endpoint, excluding the owner. Modifying this attribute while the object (or the relevant part of the object) is administratively enabled may be service impacting as egress_enabled will be temporarily set to false to apply the change. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `"no-access"`. The allowed values and their meaning are:

<pre>
"no-access" - Disallows all access.
"read-only" - Read-only access to the messages.
"consume" - Consume (read and remove) messages.
"modify-topic" - Consume messages or modify the topic/selector.
"delete" - Consume messages, modify the topic/selector or delete the Client created endpoint altogether.
</pre>
- `redelivery_delay_enabled` (Boolean) Enable or disable a message redelivery delay. When false, messages are redelivered as-soon-as-possible.  When true, messages are redelivered according to the initial, max and multiplier.  This should only be enabled when redelivery is enabled. Modifying this attribute while the object (or the relevant part of the object) is administratively enabled may be service impacting as egress_enabled will be temporarily set to false to apply the change. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `false`. Available since SEMP API version 2.33.
- `redelivery_delay_initial_interval` (Number) The delay to be used between the first 2 redelivery attempts.  This value is in milliseconds. Modifying this attribute while the object (or the relevant part of the object) is administratively enabled may be service impacting as egress_enabled will be temporarily set to false to apply the change. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `1000`. Available since SEMP API version 2.33.
- `redelivery_delay_max_interval` (Number) The maximum delay to be used between any 2 redelivery attempts.  This value is in milliseconds.  Due to technical limitations, some redelivery attempt delays may slightly exceed this value. Modifying this attribute while the object (or the relevant part of the object) is administratively enabled may be service impacting as egress_enabled will be temporarily set to false to apply the change. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `64000`. Available since SEMP API version 2.33.
- `redelivery_delay_multiplier` (Number) The amount each delay interval is multiplied by after each failed delivery attempt.  This number is in a fixed-point decimal format in which you must divide by 100 to get the floating point value. For example, a value of 125 would cause the delay to be multiplied by 1.25. Modifying this attribute while the object (or the relevant part of the object) is administratively enabled may be service impacting as egress_enabled will be temporarily set to false to apply the change. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `200`. Available since SEMP API version 2.33.
- `redelivery_enabled` (Boolean) Enable or disable message redelivery. When enabled, the number of redelivery attempts is controlled by max_redelivery_count. When disabled, the message will never be delivered from the topic-endpoint more than once. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `true`. Available since SEMP API version 2.18.
- `reject_low_priority_msg_enabled` (Boolean) Enable or disable the checking of low priority messages against the `reject_low_priority_msg_limit`. This may only be enabled if `reject_msg_to_sender_on_discard_behavior` does not have a value of `"never"`. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `false`.
- `reject_low_priority_msg_limit` (Number) The number of messages of any priority in the Topic Endpoint above which low priority messages are not admitted but higher priority messages are allowed. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `0`.
- `reject_msg_to_sender_on_discard_behavior` (String) Determines when to return negative acknowledgments (NACKs) to sending clients on message discards. Note that NACKs cause the message to not be delivered to any destination and Transacted Session commits to fail. Modifying this attribute while the object (or the relevant part of the object) is administratively enabled may be service impacting as reject_low_priority_msg_enabled will be temporarily set to false to apply the change. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `"never"`. The allowed values and their meaning are:

<pre>
"never" - Silently discard messages.
"when-topic-endpoint-enabled" - NACK each message discard back to the client, except messages that are discarded because an endpoint is administratively disabled.
"always" - NACK each message discard back to the client, including messages that are discarded because an endpoint is administratively disabled.
</pre>
- `respect_msg_priority_enabled` (Boolean) Enable or disable the respecting of message priority. When enabled, messages contained in the Topic Endpoint are delivered in priority order, from 9 (highest) to 0 (lowest). Modifying this attribute while the object (or the relevant part of the object) is administratively enabled may be service impacting as egress_enabled and ingress_enabled will be temporarily set to false to apply the change. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `false`. Available since SEMP API version 2.8.
- `respect_ttl_enabled` (Boolean) Enable or disable the respecting of the time-to-live (TTL) for messages in the Topic Endpoint. When enabled, expired messages are discarded or moved to the DMQ. Changes to this attribute are synchronized to HA mates and replication sites via config-sync. The default value is `false`.

<a id="nestedatt--event_bind_count_threshold"></a>
### Nested Schema for `event_bind_count_threshold`

Optional:

- `clear_percent` (Number) The clear threshold for the value of this counter as a percentage of its maximum value. Falling below this value will trigger a corresponding event. This attribute may not be returned in a GET. The default value is: `60`.
- `clear_value` (Number) The clear threshold for the absolute value of this counter. Falling below this value will trigger a corresponding event. This attribute may not be returned in a GET.
- `set_percent` (Number) The set threshold for the value of this counter as a percentage of its maximum value. Exceeding this value will trigger a corresponding event. This attribute may not be returned in a GET. The default value is: `80`.
- `set_value` (Number) The set threshold for the absolute value of this counter. Exceeding this value will trigger a corresponding event. This attribute may not be returned in a GET.


<a id="nestedatt--event_reject_low_priority_msg_limit_threshold"></a>
### Nested Schema for `event_reject_low_priority_msg_limit_threshold`

Optional:

- `clear_percent` (Number) The clear threshold for the value of this counter as a percentage of its maximum value. Falling below this value will trigger a corresponding event. This attribute may not be returned in a GET. The default value is: `60`.
- `clear_value` (Number) The clear threshold for the absolute value of this counter. Falling below this value will trigger a corresponding event. This attribute may not be returned in a GET.
- `set_percent` (Number) The set threshold for the value of this counter as a percentage of its maximum value. Exceeding this value will trigger a corresponding event. This attribute may not be returned in a GET. The default value is: `80`.
- `set_value` (Number) The set threshold for the absolute value of this counter. Exceeding this value will trigger a corresponding event. This attribute may not be returned in a GET.


<a id="nestedatt--event_spool_usage_threshold"></a>
### Nested Schema for `event_spool_usage_threshold`

Optional:

- `clear_percent` (Number) The clear threshold for the value of this counter as a percentage of its maximum value. Falling below this value will trigger a corresponding event. This attribute may not be returned in a GET. The default value is: `18`.
- `clear_value` (Number) The clear threshold for the absolute value of this counter. Falling below this value will trigger a corresponding event. This attribute may not be returned in a GET.
- `set_percent` (Number) The set threshold for the value of this counter as a percentage of its maximum value. Exceeding this value will trigger a corresponding event. This attribute may not be returned in a GET. The default value is: `25`.
- `set_value` (Number) The set threshold for the absolute value of this counter. Exceeding this value will trigger a corresponding event. This attribute may not be returned in a GET.
