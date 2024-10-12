
# Healthcare Realtime RAG-Chatbot Code - Project README

## Overview

This project involves building a minimal chatbot and anomaly detection system using FastAPI, Apache Beam, Apache Flink, Kafka, and several AWS services. It also includes features for data processing, model monitoring, SMS and email notifications, and anomaly detection for sensor data. The chatbot leverages edge computing and integrates with Twilio for notifications.

### Features:
- Real-time data processing using Apache Beam and Apache Flink.
- RESTful API for receiving sensor data built using FastAPI.
- Integration with Kafka for real-time streaming of sensor data.
- SMS and Email notifications for errors and model drift using Twilio and SMTP.
- Experiment tracking and drift monitoring using MLflow.
- Scalable and robust microservices architecture using AWS services.

## Microservices Architecture

The system is built on a microservices architecture, where different functionalities are split into independent services that communicate with each other. Each microservice is designed to handle a specific task and is scalable and deployable independently.

### Microservices:
1. **Chatbot Service**:
   - Handles chat interactions with users via a FastAPI endpoint.
   - Sends user queries to the Preprocessing Service for further processing.
   
   **Endpoint**: `/chat`
   
2. **Data Ingestion Service**:
   - Responsible for ingesting data from Kafka using Apache Beam.
   - Transmits ingested data to the Preprocessing Service.
   
   **Endpoint**: `/ingest`
   
3. **Preprocessing Service**:
   - Handles data preprocessing tasks such as windowing and feature extraction.
   - Processes both user queries and ingested data for further analysis.
   
   **Endpoint**: `/preprocess`
   
4. **Model Drift Control Service**:
   - Monitors the model for concept drift.
   - Retrains the model when drift is detected.
   
   **Endpoint**: `/check_drift`
   
5. **RAG (Retrieval-Augmented Generation) Service**:
   - Retrieves relevant documents from a knowledge base based on the user's query.
   - Uses the retrieved information to generate responses.
   
   **Endpoint**: `/retrieve`

### Communication Between Microservices:
- The services communicate via HTTP REST API calls.
- The Chatbot Service calls the Preprocessing and RAG services to preprocess queries and retrieve documents, respectively.
- The Data Ingestion Service communicates with the Preprocessing Service for real-time data flow.
  
## Prerequisites

1. Python 3.7+
2. Docker (for running Kafka, Zookeeper, and other dependencies)
3. Google Cloud SDK (if using Apache Beam's Dataflow Runner)
4. AWS account for using SageMaker, MSK, and other AWS services
5. Kafka setup (local or cloud-based)

### Environment Variables

The application requires the following environment variables to be set for different services to function correctly:

- Kafka Configuration:
  - `KAFKA_BOOTSTRAP_SERVERS`: Bootstrap servers for Kafka (e.g., `localhost:9092`).

- Flink Configuration:
  - `FLINK_JOBMANAGER_ADDRESS`: Address of Flink Job Manager.

- Twilio Configuration (For SMS Notifications):
  - `TWILIO_ACCOUNT_SID`: Twilio account SID.
  - `TWILIO_AUTH_TOKEN`: Twilio Auth Token.
  - `TWILIO_PHONE_NUMBER`: Twilio phone number to send messages.
  - `NOTIFICATION_PHONE_NUMBER`: Phone number to receive SMS notifications.

- Email Configuration (SMTP server details):
  - `SMTP_SERVER`: SMTP server address (e.g., `smtp.gmail.com`).
  - `SMTP_PORT`: SMTP server port (e.g., `587`).
  - `SMTP_USERNAME`: Username for the SMTP server.
  - `SMTP_PASSWORD`: Password for the SMTP server.

## Running the Project

1. Clone the repository:

```sh
git clone https://github.com/your-repo/chatbot-project.git
```

2. Set up environment variables for Kafka, Flink, Twilio, and SMTP as described in the "Environment Variables" section.

3. Start each microservice using Docker or directly using `uvicorn`:

```sh
# Start the chatbot service
uvicorn chatbot_service:app --reload

# Start the data ingestion service
uvicorn data_ingestion_service:app --reload

# Start the preprocessing service
uvicorn preprocessing_service:app --reload

# Start the model drift control service
uvicorn model_drift_control_service:app --reload

# Start the RAG service
uvicorn rag_service:app --reload
```

4. (Optional) Use Docker Compose to manage and run all services at once.

## Testing

Unit tests are included for the FastAPI endpoints and the data pipelines.

To run the tests:

```sh
pytest
```

## Improvements Implemented

1. **Conversation Memory Optimization**:
   - The chatbot's conversation memory is optimized using a summary-based approach to keep memory usage low.

2. **Model Drift Monitoring**:
   - Implemented a model drift monitoring mechanism using MLflow to track F1 scores and trigger retraining notifications if drift is detected.

3. **Data Leakage Control**:
   - Proper dataset splitting has been implemented to control data leakage. Validation sets are separated from training data to ensure no overlap.

4. **Testing and Continuous Integration**:
   - Added unit tests for major components like the FastAPI API, Kafka integration, Beam, and Flink processing.
   - Implemented a Continuous Integration (CI) pipeline to automatically run tests.

5. **Notifications Integration**:
   - SMS and email notifications are implemented to notify the user in case of pipeline errors, model drift, or other critical issues.

## Future Work

1. **Containerization**:
   - Use Docker to containerize the application and ensure consistency in deployment across different environments.

2. **Deployment**:
   - Deploy the FastAPI app, Beam, and Flink jobs on AWS ECS or Kubernetes for better scaling.

3. **Scaling Kafka**:
   - Use AWS MSK to scale Kafka and manage the cluster with automated monitoring.

4. **Authentication and Security**:
   - Implement OAuth or JWT for API authentication.
   - Secure Kafka with SSL/TLS and configure access control for topics.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.



