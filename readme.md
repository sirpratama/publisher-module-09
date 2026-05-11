# Publisher

## Questions

### a. How much data will your publisher program send to the message broker in one run?

In one run, the publisher sends **5 events** to the message broker. Each event is a `UserCreatedEventMessage` containing two fields: a `user_id` (integers 1–5) and a `user_name` (e.g., `2406453556-Amir`, `2406453556-Budi`, `2406453556-Cica`, `2406453556-Dira`, `2406453556-Emir`). So 5 separate messages are published to the `user_created` queue on each execution.

### b. The URL `amqp://guest:guest@localhost:5672` is the same as in the subscriber — what does it mean?

Both the publisher and the subscriber use the **exact same broker URL**, which means they are both connecting to the same RabbitMQ instance running on `localhost:5672`. This is the core idea of event-driven architecture: the publisher and subscriber do **not** communicate with each other directly. Instead, they both connect to the same shared message broker. The publisher sends events to the broker, and the subscriber reads and processes those events from the broker. They are fully decoupled — neither needs to know about the other's existence.

## Running RabbitMQ as Message Broker

RabbitMQ is running via Docker on `localhost:5672` (AMQP) and `localhost:15672` (management UI). The screenshot below shows the management dashboard confirming the broker is active and ready to accept connections.

![RabbitMQ Running](images/rabbitmq.png)

## Sending and Processing Event

When the publisher runs (`cargo run`), it sends 5 events to the `user_created` queue on RabbitMQ. The subscriber, which is already listening, receives and processes each event one by one, printing the message to the console.

**Subscriber console** — messages received from the broker:

![Subscriber Console](images/Screenshot%202026-05-11%20233903.png)

**Publisher run** — successfully compiled and sent all 5 events:

![Publisher Run](images/Screenshot%202026-05-11%20233939.png)

## Monitoring Chart Based on Publisher

Each time the publisher runs, it sends 5 events to RabbitMQ. The spike visible in the RabbitMQ management chart below corresponds to those bursts of messages being published. The more times the publisher runs in quick succession, the more spikes appear on the message rate chart.

![RabbitMQ Spike](images/purple%20spike.png)
