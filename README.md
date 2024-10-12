
# Minimal Chatbot Code - Project README

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
   
   **Code Snippet**:
   ```python
{chatbot_code[:400]}...
   ```

2. **Data Ingestion Service**:
   - Responsible for ingesting data from Kafka using Apache Beam.
   - Transmits ingested data to the Preprocessing Service.
   
   **Endpoint**: `/ingest`
   
   **Code Snippet**:
   ```python
{data_ingestion_code[:400]}...
   ```

3. **Preprocessing Service**:
   - Handles data preprocessing tasks such as windowing and feature extraction.
   - Processes both user queries and ingested data for further analysis.
   
   **Endpoint**: `/preprocess`
   
   **Code Snippet**:
   ```python
{preprocessing_code[:400]}...
   ```

4. **Model Drift Control Service**:
   - Monitors the model for concept drift.
   - Retrains the model when drift is detected.
   
   **Endpoint**: `/check_drift`
   
   **Code Snippet**:
   ```python
{model_drift_code[:400]}...
   ```

5. **RAG (Retrieval-Augmented Generation) Service**:
   - Retrieves relevant documents from a large corpus for better chatbot responses.
   
   **Endpoint**: `/retrieve`
   
   **Code Snippet**:
   ```python
{rag_code[:400]}...
   ```

## Tests

Testing of the microservices and the data pipelines is conducted using pytest.

To run the tests:

```sh
pytest
```

**Test Code Snippet**:
```python
{test_code[:400]}...
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

## Contact

If you have any questions or need help getting started, feel free to reach out!

**Email**: [your_email@example.com]  
**GitHub**: [your_github_username]

---

Happy coding! 😊
