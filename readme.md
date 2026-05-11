# Publisher

## Questions

### a. How much data will your publisher program send to the message broker in one run?

In one run, the publisher sends **5 events** to the message broker. Each event is a `UserCreatedEventMessage` containing two fields: a `user_id` (integers 1–5) and a `user_name` (e.g., `2406453556-Amir`, `2406453556-Budi`, `2406453556-Cica`, `2406453556-Dira`, `2406453556-Emir`). So 5 separate messages are published to the `user_created` queue on each execution.

### b. The URL `amqp://guest:guest@localhost:5672` is the same as in the subscriber — what does it mean?

Both the publisher and the subscriber use the **exact same broker URL**, which means they are both connecting to the same RabbitMQ instance running on `localhost:5672`. This is the core idea of event-driven architecture: the publisher and subscriber do **not** communicate with each other directly. Instead, they both connect to the same shared message broker. The publisher sends events to the broker, and the subscriber reads and processes those events from the broker. They are fully decoupled — neither needs to know about the other's existence.

## Running RabbitMQ as Message Broker

RabbitMQ is running via Docker on `localhost:5672` (AMQP) and `localhost:15672` (management UI). The screenshot below shows the management dashboard confirming the broker is active and ready to accept connections.

![RabbitMQ Running](images/rabbitmq.png)
