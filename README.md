# Simple Message Broker in Go

This project implements a basic message broker in Go. It allows you to create topics, subscribe to them, publish messages, and unsubscribe from them. It demonstrates the core concepts of message brokering with minimal overhead.

## Features

- **Publish-Subscribe Model**: Supports topics where subscribers receive messages published to those topics.
- **Channel-Based Communication**: Uses Go channels for message delivery between the broker and subscribers.
- **Automatic Unsubscribe for Slow Subscribers**: Automatically unsubscribes slow subscribers if they do not process messages within a specified timeout.

## Prerequisites

- Go 1.18 or later

## Installation

1. **Clone the repository:**

   ```bash
   git clone https://github.com/yourusername/simple-message-broker.git
   cd simple-message-broker
   ```

2. **Build the application:**

   ```bash
   go build -o message_broker
   ```

3. **Run the application:**

   ```bash
   ./message_broker
   ```

   This will execute the main function and demonstrate the broker's functionality.

## Code Overview

- **`message_broker.go`**: The main file containing the implementation of the message broker.

- **Types**:
  - `Message`: Represents a message with a topic and a payload.
  - `Subscriber`: Represents a subscriber with a channel to receive messages and an unsubscribe channel.
  - `Broker`: Represents the message broker that manages subscribers and handles message publishing.

- **Functions**:
  - `NewBroker() *Broker`: Creates a new instance of the Broker.
  - `(*Broker) Subscribe(topic string) *Subscriber`: Subscribes to a topic and returns a subscriber.
  - `(*Broker) Unsubscribe(topic string, subscriber *Subscriber)`: Unsubscribes a subscriber from a topic.
  - `(*Broker) Publish(topic string, payload interface{})`: Publishes a message to a topic.

- **Main Function**:
  - Creates a new broker instance.
  - Subscribes a subscriber to the topic "example_topic".
  - Launches a goroutine to listen for messages and handle unsubscription.
  - Publishes a few test messages.
  - Unsubscribes the subscriber and ensures that no further messages are received.

## Example Usage

1. **Subscription and Message Handling**:

   The example subscribes to the topic "example_topic" and prints any received messages. It also handles unsubscription when the channel is closed or the unsubscribe signal is received.

2. **Publishing Messages**:

   Messages are published to the topic "example_topic", and subscribers will receive them unless they are slow, in which case they are automatically unsubscribed.

3. **Automatic Unsubscription**:

   Subscribers that do not process messages within one second are automatically unsubscribed, and a message is logged.

## Notes

- **Concurrency**: The broker handles concurrent subscribers and messages using Go's concurrency features like goroutines and channels.
- **Timeout Handling**: If a subscriber is slow, the broker automatically unsubscribes it to prevent delays in message processing.

## Contributing

Feel free to fork the repository and submit pull requests for improvements or bug fixes.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
