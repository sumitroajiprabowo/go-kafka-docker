### Create Topic

```
docker compose exec broker \
  kafka-topics --create \
    --topic purchases \
    --bootstrap-server localhost:9092 \
    --replication-factor 1 \
    --partitions 1
```

### Install Dependencies

Before building the code, you may need to download the Confluent Go Kafka dependency with:
```
go get github.com/confluentinc/confluent-kafka-go/kafka
```
### Build Producer

You can test the syntax before proceeding by compiling with:
```
go build -o out/producer util.go producer.go
```
### Build Consumer

You can test the consumer syntax by compiling with:
```
go build -o out/consumer util.go consumer.go
```
### Produce Events

First be sure you have successfully compiled the producer code with:
```
go build -o out/producer util.go producer.go
```
In order to run the producer, execute the compiled binary passing in the configuration file created above:
```
./out/producer getting-started.properties
```
You should see output that resembles:
```
Produced event to topic purchases: key = awalther   value = t-shirts
Produced event to topic purchases: key = awalther   value = batteries
Produced event to topic purchases: key = jsmith     value = gift card
Produced event to topic purchases: key = jsmith     value = book
Produced event to topic purchases: key = htanaka    value = book
Produced event to topic purchases: key = sgarcia    value = alarm clock
Produced event to topic purchases: key = eabara     value = batteries
Produced event to topic purchases: key = htanaka    value = batteries
Produced event to topic purchases: key = jbernard   value = book
Produced event to topic purchases: key = awalther   value = alarm clock
```
## Consume Events

From another terminal, run the following command to run the consumer application which will read the events from the purchases topic and write the information to the terminal.
```
`./out/consumer getting-started.properties `
```
The consumer application will start and print any events it has not yet consumed and then wait for more events to arrive. On startup of the consumer, you should see output that resembles the below. Once you are done with the consumer, press ctrl-c to terminate the consumer application.
```
Consumed event from topic purchases: key = jsmith     value = alarm clock
Consumed event from topic purchases: key = htanaka    value = book
Consumed event from topic purchases: key = eabara     value = batteries
Consumed event from topic purchases: key = htanaka    value = t-shirts
Consumed event from topic purchases: key = htanaka    value = t-shirts
Consumed event from topic purchases: key = htanaka    value = gift card
Consumed event from topic purchases: key = sgarcia    value = gift card
Consumed event from topic purchases: key = jbernard   value = gift card
Consumed event from topic purchases: key = awalther   value = alarm clock
Consumed event from topic purchases: key = htanaka    value = book
```

