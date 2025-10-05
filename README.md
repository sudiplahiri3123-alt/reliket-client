# reliket-client

A lightweight client library for Reliket message queue system.

## Installation

```bash
npm install reliket-client

````
## Features

- Simple API for producing and consuming messages
- Supports JSON and plain text messages
- Automatic handling of connection and subscriptions
- Lightweight TCP client under the hood


### Usage examples

Find below the usage of reliket-client package with simple code snippets:


### Producer

```js
const { ReliketProducer } = require('reliket-client');

(async () => {
  const producer = new ReliketProducer();
  await producer.connect();
  await producer.send({
    topic: 'my-topic',
    messages: [{ value: 'Hello world!' }]
  });
  await producer.disconnect();
})();

```
### Consumer

```js
const { ReliketConsumer } = require('reliket-client');

(async () => {
  const consumer = new ReliketConsumer({ topic: 'my-topic' });
  await consumer.connect();
  await consumer.run({
    eachMessage: async ({ topic, message }) => {
      console.log(`[${topic}] ${message}`);
    }
  });
})();

```

## API Reference

### ReliketProducer

- `connect()`: Establishes a connection to the Reliket server.

- `send({ topic, messages })`: Sends one or multiple messages to the specified topic.
  - `topic` (string): The topic name.
  - `messages` (array): Array of message objects, each with a `value` property (string or JSON).

- `disconnect()`: Gracefully closes the connection.

### ReliketConsumer

- `connect()`: Connects and subscribes to the configured topic.

- `run({ eachMessage })`: Starts the consumer loop, calling the `eachMessage` callback for each received message.
  - `eachMessage` is an async function with `{ topic, message }` as parameters.

- `disconnect()`: Unsubscribes and closes the connection.



### f. License

```js
MIT © sudtechno_master
```
