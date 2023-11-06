# Real-Time Stock Market Data Pipeline with Kafka, S3, and Athena

This project builds an end-to-end data pipeline to ingest and analyze real-time stock market data using Apache Kafka, Amazon S3, AWS Glue, and Athena.

## Architecture

The architecture follows this flow:

1. Kafka Producer fetches stock market data from a CSV file and publishes it to a Kafka topic
2. Kafka Consumer subscribes to the topic and writes each message to a JSON file in an S3 bucket
3. AWS Glue crawls the S3 bucket periodically and catalogs the data
4. Athena allows running SQL queries on the parsed JSON data in S3

### Kafka Setup

- Kafka and Zookeeper are installed locally on an EC2 instance
- A Kafka topic `demo_testing2` is created
- Kafka Producer notebook reads stock market data from a CSV file and publishes JSON messages to the topic 
- Kafka Consumer notebook subscribes to the topic and writes each message to an S3 bucket

### S3 Setup

- An S3 bucket is created to store the JSON files
- Kafka consumer writes each message to a separate JSON file in the bucket
- File names are prefixed with "stock_market_"

### Glue Setup

- AWS Glue crawls the S3 bucket periodically to infer schema and create tables
- This allows querying the data with Athena

### Athena Setup

- With the AWS Glue catalog, Athena can query the JSON data in S3 with standard SQL
- Provides the ability to analyze ingested data interactively with low latency

## Running the Project

To run the project end-to-end:

1. Start Zookeeper and Kafka server on EC2
2. Run the Kafka producer notebook to publish data 
3. Run the Kafka consumer notebook to write messages to S3 
4. Setup AWS Glue crawl on the S3 bucket
5. Use Athena to run SQL queries on ingested data

The notebooks provide examples for producing and consuming messages with Kafka in Python.

## Next Steps

Some ways to extend the project:

- Use larger real-time data sources for stock market data
- Optimize Kafka performance for high-volume data ingestion
- Visualize data with QuickSight or other BI tools
- Apply machine learning models to the data for insights
