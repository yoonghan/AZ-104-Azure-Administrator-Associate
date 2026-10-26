# Application Architecture

## Service Bus
- Push and Pull
- Have Queue and Topic
- Reliable messaging.

## Event Hub
- Only support Pull
- like Kafka
- Big data streaming. Massive data.

## Event Grid
- Only support Push
- Event-driven. Trigger function when event happens.
- Event routing.

## Key Differences

| Feature | Azure Event Hubs | Azure Service Bus |
| :--- | :--- | :--- |
| **Primary Purpose** | Big data streaming and telemetry ingestion | Enterprise message brokering and workflows |
| **Core Philosophy** | "Something has happened" (announcement) | "Do something" or "Give me something" (command/task) |
| **Message Lifespan** | Retained for a set period (default 7 days); not deleted when read | Deleted or completed by the receiver after processing |
| **Throughput Scale** | Millions of events per second | Thousands of messages per second |
| **Ordering & Sessions** | Ordered within individual partitions | Strict FIFO ordering with message sessions |
| **Reliability & Guarantees** | High-speed stream; individual message drops/skips can happen in massive scale | At-least-once or transactions, duplicate detection, dead-letter queues |
| **Replay Capability** | Yes—consumers can re-read the stream by changing their offset/index | No—messages leave the queue once consumed and acknowledged |


## Pricing Tier

|Azure Event Hubs|Azure Service Bus|
| --- | --- |
|**Basic**|256 KB|256 KB (Queues only)|
|**Standard**|1 MB|256 KB|
|**Premium**|1 MB|Up to 100 MB (Requires AMQP protocol)|
|**Dedicated**|Up to 20 MB (Self-serve clusters)|N/A (Uses Premium tier clustering)|

1. Note A standard queue has a maximum size cap of 80 GB if partitioned. Your 320 GB peak requirement will cause a Standard queue to fill up completely, resulting in the broker rejecting new incoming messages with a "Quota Exceeded" exception.

## Alternatives
1. Storage Queue is alternative for Service Bus Queue. Choose Azure Storage Queues if:

  - Your system does not care about strict FIFO ordering
  - handle the occasional duplicate message

| Feature | Azure Storage Queues| Azure Service Bus (Premium)|
| --- | --- |---|
| **Total Message Limit**|Virtually unlimited (Up to 5 PB total account size) [1]|Maxes out at 1 TB per namespace unit [5]|
| **320 GB Storage Cost**|Extremely cheap ($0.05 to $0.15 per GB/month)|Expensive (Requires flat monthly premium tier fee)|
| **Ordering (FIFO)**|Not guaranteed (Best-effort ordering only) [1, 2]|Strict FIFO guaranteed (Using Message Sessions) [1, 2]|
| **Duplicate Detection**|No (At-least-once delivery; apps must handle duplicates) [2]|Yes (Native duplicate detection built-in) [1, 2]|
| **Dead-Letter Queues**|No (You must manually move poisoned messages) [2]|Yes (Automatic isolation of broken messages) [1, 2]|

## Cache aside
1. Always check cache first. If cache miss, get from DB and write to cache.
2. In Azure, use Azure Cache for Redis.

