# Realtime Data Streaming | End-to-End Data Engineering Project
This project was conducted by @airscholar, thank you for your help on making this possible.

![Data engineering architecture](https://github.com/chachestriki/data-engineering/assets/56995207/567ff732-6337-4b8a-a34b-c526aaf606bb)

# System Architecture Overview

![System Architecture](path/to/image.png)

## Overview

This document provides an overview of the data pipeline system architecture. The architecture is designed for real-time data ingestion, processing, and storage using various technologies.

## Components

1. **Data Source (API)**
   - **API:** The data source from which data is fetched. This could be any external API providing the data to be ingested into the pipeline.

2. **Airflow**
   - **Airflow:** Used for workflow orchestration. It schedules and manages tasks such as fetching data from the API, processing it, and streaming it to Kafka.
   - **PostgreSQL:** Airflow uses PostgreSQL to store metadata about the workflows, tasks, and their states.

3. **Kafka**
   - **Zookeeper:** Manages the Kafka brokers and helps maintain the distributed nature of Kafka.
   - **Kafka Broker:** Handles the actual data streams. It receives and stores data records and serves consumers.
   - **Control Center:** A tool provided by Confluent for monitoring and managing Kafka clusters.
   - **Schema Registry:** Manages Avro schemas used for Kafka topics, ensuring compatibility between producers and consumers.

4. **Spark**
   - **Spark Master:** The master node that manages the Spark cluster.
   - **Spark Workers:** Worker nodes that perform the data processing tasks. They receive data from Kafka, process it, and prepare it for storage.

5. **Cassandra**
   - **Cassandra:** A NoSQL database designed for high availability and scalability. It stores the processed data from Spark for efficient querying.

6. **Docker**
   - **Docker:** The entire setup is containerized using Docker. This ensures consistency across environments and simplifies deployment and scaling.

## Data Flow

1. **Data Ingestion:**
   - Data is fetched from the external API by Airflow.
   - The fetched data is then formatted and sent to a Kafka topic.

2. **Real-Time Data Processing:**
   - Spark consumes data from the Kafka topic.
   - Spark processes the data and transforms it as required.

3. **Data Storage:**
   - The processed data is then streamed from Spark to Cassandra for storage.

## Key Points

- **Workflow Orchestration:** Airflow manages the workflows, ensuring that data is fetched, processed, and stored in a timely and efficient manner.
- **Stream Processing:** Kafka acts as the central hub for data streams, allowing for real-time processing with Spark.
- **Schema Management:** The Schema Registry ensures that the data structure is consistent and compatible across different components.
- **Monitoring and Management:** Confluent Control Center provides a UI for monitoring the health and performance of the Kafka cluster.
- **Scalability:** Using Docker, the entire system can be easily scaled horizontally, adding more Spark workers or Kafka brokers as needed.

## Docker Compose Configuration

The Docker Compose setup orchestrates the various components, ensuring they are properly configured and networked. Key services include:
- **Zookeeper**
- **Kafka Broker**
- **Schema Registry**
- **Control Center**
- **Airflow (Webserver and Scheduler)**
- **PostgreSQL**
- **Spark (Master and Workers)**
- **Cassandra**

This architecture ensures a robust, scalable, and efficient data pipeline for real-time data processing and storage.
