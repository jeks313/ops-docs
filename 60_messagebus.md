<!-- Space: OP -->
<!-- Parent: Operational Readiness Review -->
<!-- Title: OPR - Message Bus -->

# Message Bus

- A single topic should contain a single schema of events or messages. Do not mix message types on the same topic
- Messages on a topic should be atomic units representing a single datum or event. Do NOT have messages that themselves are arrays of messages. This is because it is then impossible to reason about the meaning of a queue in such circumstances. If each message on the bus could be 1, 10 or 10,000 events or messages, you have no way of telling how much work a queue represents and it is impossible to set timings and timeouts appropriately. Make each message a unit of work.
- Consumers must provide an endpoint to process a single message. Do not ever just write message bus consumer code. Doing so makes it much harder to test your code as you need the bus, topic, consumer and target to test. It also makes operating the service very hard, as a single message is impossible to test in production. If you have a bad message, or you wish to test the downstream part of a consumer, you make it almost impossible to do if there is not a way to consume a single message without the bus on demand. Provide either a REST endpoint or a command line input (via stdin or filename input) with your consumer service.
- It is a preferable design to just provide REST endpoints for consuming messages and encapsulate message bus logic and code in a separate service. This scales to billions of messages.
- It is not a good idea to implement retry logic inside your consumer. All good message bus systems already implement timeouts and retries much more reliably than you ever will. Fail fast and leave the message on the queue.
- Ensure that messages that you fail on are removed from the queue and submitted to dead letter queues. If you fail to process a message and this is a permanent fail do not let it retry - remove it from the queue and submit to a dead letter queue.
- Measure performance and create single message processors first. Only batch message processing if absolutely necessary. Batch processing introduces many failure and retry states that are hard to reason about from an operations perspective.
