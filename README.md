# Event-driven scheduling of Airflow DAGs with Apache Kafka

This project demonstrates [event-driven scheduling](https://www.astronomer.io/docs/learn/airflow-event-driven-scheduling/) using Apache Kafka and Apache Airflow.

This project works out of the box when using the [Astro CLI](https://www.astronomer.io/docs/astro/cli/install-cli) spinning up a full local Airflow environment with an additional local Kafka container. 

## Project Structure

```text
├── dags/
│   ├── event_driven_dag.py    # Event-driven DAG that runs as soon as a message appears in a Kafka topic
│   └── producer_dag.py        # Producer DAG that sends messages to Kafka
├── tests/
│   └── dags/
│       └── test_dag_example.py # example DAG tests
├── docker-compose.override.yml # Kafka container configuration
├── Dockerfile                 # Astro CLI image
└── requirements.txt          # Python dependencies (provider packages)
```


## Local Development Setup

1. Fork this repository and clone it to your local machine.

2. Make sure you have the [Astro CLI](https://www.astronomer.io/docs/astro/cli/install-cli) installed and are at least on version 1.34.0 (check with `astro version`) to run Airflow 3 projects.

3. Create a `.env` file in the root of your project and copy the contents from `.env_example` to it. This environment variable defines the connection between Kafka and Airflow.

4. Start the project by running `astro dev start`. Note that it takes a bit longer for Kafka to start up even after Airflow is ready.

5. Unpause the `event_driven_dag` to have it start listening for messages

6. Manually trigger the `producer_dag` to send test messages to the Kafka topic

7. See the `event_driven_dag` run and print the message to the logs.