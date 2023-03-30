# ETL Pipeline for Tweets and News using Python, Kafka, AWS and ELK Stack

## Architecture of the application

![arch](assets/architecture.png)

## Running the ETL Pipeline

### Step 1: Start Kafka, Elastic Search and Kibana

Run the following command to start the kafka brokers with the zookeeper, Elastic Search and Kibana

```sh
docker compose up
```

### Step 2: Extract

To extract data from the source, you need to run the following commands in different terminal

```sh
python3 extract/tweet_producer.py
```

```sh
python3 extract/news_producer.py
```

To check if the producer produces any data, run the following commands in different terminal

```sh
kafka-console-consumer.sh --topic Tweets_Topic --bootstrap-server localhost:9092 --from-beginning

or

kafka-console-consumer.sh --topic News_Topic --bootstrap-server localhost:9092 -from-beginning
```

If it produces any data then the extract part is working fine.

### Step 3: Transform

After extracting the data from the source, you need to run the following commands in different terminal to transform the data and add sentiment prediction to the data

```sh
python3 transform/tweet_transformer.py
```

```sh
python3 transform/news_transformer.py
```

To check if it transforms the data, run

```sh
kafka-console-consumer.sh --topic Processed --bootstrap-server localhost:9092 --from-beginning
```

If the messages has `sentiment` in it then the transformers works fine.
