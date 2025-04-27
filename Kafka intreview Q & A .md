# Apache Kafka Interview Questions and Answers

## 1. What is Apache Kafka and why is it used?
Apache Kafka is a distributed streaming platform used for building real-time data pipelines and streaming applications.

## 2. How does Kafka differ from traditional messaging systems?
Kafka is designed for fault tolerance, high throughput, and scalability, unlike traditional messaging systems that may not handle large data streams efficiently.

## 3. What are Producers and Consumers in Kafka?
- **Producers** publish messages to Kafka topics.
- **Consumers** read messages from topics.

```java
// Producer
producer.send(new ProducerRecord<String, String>("topic", "key", "value"));

// Consumer
consumer.subscribe(Arrays.asList("topic"));
```

## 4. What is a Kafka Topic?
A Topic is a category to which records are published by producers and from which records are consumed by consumers.

```bash
kafka-topics.sh --create --topic my_topic --bootstrap-server localhost:9092
```

## 5. How does Kafka ensure durability and fault-tolerance?
Kafka replicates data across multiple brokers. Consumers read from leader replicas, and follower replicas synchronize data.

## 6. What is a Kafka Partition?
Partitions allow Kafka to horizontally scale as each partition can be hosted on a different server.

## 7. What is Zookeeper’s role in a Kafka ecosystem?
Zookeeper manages brokers, maintains metadata, and helps in leader election for partitions.

## 8. How can you secure Kafka?
Kafka can be secured using SSL for encryption, SASL for authentication, and ACLs for authorization.

## 9. What is Kafka Streams?
Kafka Streams is a client library for building real-time, highly scalable, fault-tolerant stream processing applications.

```java
KStream<String, String> stream = builder.stream("input-topic");
stream.to("output-topic");
```

## 10. What are some use-cases for Kafka?
- Real-time analytics
- Data lakes
- Aggregating data from different sources
- Acting as a buffer to handle burst data loads

## 11. How do you integrate Kafka with Spring Boot?
Use the Spring Kafka library, which provides `@KafkaListener` for consumers and `KafkaTemplate` for producers.

```java
@KafkaListener(topics = "myTopic")
public void listen(String message) {
    // Handle message
}
```

## 12. How do you send a message to a Kafka topic using Spring Kafka?
Use `KafkaTemplate` to send messages.

```java
kafkaTemplate.send("myTopic", "myMessage");
```

## 13. How do you consume messages from a Kafka topic in Spring?
Use the `@KafkaListener` annotation to mark a method as a Kafka message consumer.

```java
@KafkaListener(topics = "myTopic")
public void consume(String message) {
    // Process message
}
```

## 14. How do you handle message deserialization errors in Spring Kafka?
Use the `ErrorHandlingDeserializer` to wrap the actual deserializer and catch deserialization errors.

## 15. How do you ensure ordered message processing in Spring Kafka?
Set the `concurrency` property of `@KafkaListener` to 1 to ensure single-threaded consumption for each partition.

```java
@KafkaListener(topics = "myTopic", concurrency = "1")
```

## 16. How do you batch-process messages from Kafka in Spring?
Use the `@KafkaListener` annotation with the `batchListener` property set to `true`.

```java
@KafkaListener(topics = "myTopic", batchListener = true)
public void consume(List<String> messages) {
    // Process messages
}
```

## 17. How do you filter messages in Spring Kafka?
Implement a `RecordFilterStrategy` to filter out unwanted records before they reach the `@KafkaListener`.

### RecordFilterStrategy Implementation
```java
import org.apache.kafka.clients.consumer.ConsumerRecord;
import org.springframework.kafka.listener.adapter.RecordFilterStrategy;

public class MyRecordFilterStrategy implements RecordFilterStrategy<String, String> {

    @Override
    public boolean filter(ConsumerRecord<String, String> consumerRecord) {
        return !consumerRecord.value().contains("important");
    }
}
```

### Kafka Listener Container Factory Configuration
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.kafka.config.ConcurrentKafkaListenerContainerFactory;
import org.springframework.kafka.core.ConsumerFactory;

@Configuration
public class KafkaConsumerConfig {

    @Bean
    public ConcurrentKafkaListenerContainerFactory<String, String> kafkaListenerContainerFactory(
            ConsumerFactory<String, String> consumerFactory) {
        ConcurrentKafkaListenerContainerFactory<String, String> factory = new ConcurrentKafkaListenerContainerFactory<>();
        factory.setConsumerFactory(consumerFactory);
        factory.setRecordFilterStrategy(new MyRecordFilterStrategy());
        return factory;
    }
}
```

## 18. How do you handle retries for message processing in Spring Kafka?
Configure a `SeekToCurrentErrorHandler` or implement a custom error handler to manage retries.

## 19. How can you produce and consume Avro messages in Spring Kafka?
Use the Apache Avro serializer and deserializer along with Spring Kafka’s `KafkaTemplate` and `@KafkaListener`.

## 20. How do you secure Kafka communication in a Spring application?
Configure SSL properties in the `application.yml` or `application.properties` file.

```yaml
spring.kafka.properties.security.protocol: SSL
```

## 21. What are the key differences between Spring AMQP and Spring Pub-Sub?
- **Spring AMQP**: Based on the AMQP protocol, suitable for RabbitMQ.
- **Spring Pub-Sub**: Geared towards high-throughput data streaming like Kafka.

## 22. How do message delivery semantics differ between Spring AMQP and Spring Pub-Sub?
- **Spring AMQP**: Granular control over acknowledgment and transactions.
- **Spring Pub-Sub**: Focus on high-throughput with support for at-least-once, at-most-once, and exactly-once delivery.

### Exactly-Once Producer Example
```java
import org.apache.kafka.clients.producer.*;

import java.util.Properties;

public class ExactlyOnceProducer {
    public static void main(String[] args) {
        Properties props = new Properties();
        props.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, "localhost:9092");
        props.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringSerializer");
        props.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringSerializer");
        props.put(ProducerConfig.TRANSACTIONAL_ID_CONFIG, "my-transactional-id");
        props.put(ProducerConfig.ACKS_CONFIG, "all");

        Producer<String, String> producer = new KafkaProducer<>(props);
        producer.initTransactions();

        try {
            producer.beginTransaction();
            for (int i = 0; i < 100; i++) {
                producer.send(new ProducerRecord<>("my-topic", Integer.toString(i), Integer.toString(i)));
            }
            producer.commitTransaction();
        } catch (Exception e) {
            producer.abortTransaction();
        }
        producer.close();
    }
}
```

### Exactly-Once Consumer Example
```java
import org.apache.kafka.clients.consumer.*;

import java.time.Duration;
import java.util.Collections;
import java.util.Properties;

public class ExactlyOnceConsumer {
    public static void main(String[] args) {
        Properties props = new Properties();
        props.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, "localhost:9092");
        props.put(ConsumerConfig.GROUP_ID_CONFIG, "my-group");
        props.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringDeserializer");
        props.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringDeserializer");
        props.put(ConsumerConfig.ISOLATION_LEVEL_CONFIG, "read_committed");

        Consumer<String, String> consumer = new KafkaConsumer<>(props);
        consumer.subscribe(Collections.singletonList("my-topic"));

        while (true) {
            ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(100));
            records.forEach(record -> {
                System.out.printf("Consumed record with key %s and value %s%n", record.key(), record.value());
            });
        }
    }
}
```

## 23. How do you handle message ordering in Spring AMQP and Spring Pub-Sub?
- **Spring AMQP**: Message ordering maintained within a single queue.
- **Spring Pub-Sub (Kafka)**: Ordering maintained within each partition.

## 24. How do you implement dead-letter queues in Spring AMQP and Spring Pub-Sub?
- **Spring AMQP**: Built-in support for DLQs.
- **Spring Pub-Sub**: Use a separate topic for DLQs.

### Dead-Letter Queue Handling in Spring Kafka

```java
@KafkaListener(topics = "my-topic", errorHandler = "myErrorHandler")
public void listen(String message) {
    // Process message or throw an exception
}

@Bean
public KafkaTemplate<String, String> kafkaTemplate() {
    return new KafkaTemplate<>(producerFactory());
}

@Bean
public ProducerFactory<String, String> producerFactory() {
    // Configure producer factory
}

@Bean
public MyErrorHandler myErrorHandler(KafkaTemplate<String, String> template) {
    return new MyErrorHandler(template);
}

public class MyErrorHandler implements ErrorHandler {

    private final KafkaTemplate<String, String> template;

    public MyErrorHandler(KafkaTemplate<String, String> template) {
        this.template = template;
    }

    @Override
    public void handle(Exception thrownException, ConsumerRecord<?, ?> record) {
        template.send("my-dead-letter-topic", record.key().toString(), record.value().toString());
    }
}
```

## 25. How do Spring AMQP and Spring Pub-Sub handle message filtering?
- **Spring AMQP**: Supports routing options like direct, topic, fanout, and headers.
- **Spring Pub-Sub (Kafka)**: Rely on consumer logic or Kafka Streams for complex filtering.

---

### Closing Thoughts
In the ever-evolving landscape of backend engineering, Apache Kafka stands as a beacon for real-time data processing and streaming. As Java backend engineers, understanding Kafka is not just a skill but a necessity in today’s data-driven world. From the simplicity of producing and consuming messages to the complexities of ensuring data durability and fault tolerance, Kafka offers a robust platform for scalable applications. As we continue to explore the depths of real-time data streaming, may our understanding of Kafka deepen, and our applications become more resilient.

Until next time, keep streaming and stay curious!

