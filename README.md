# End-to-End Batch and Streaming Data Pipeline on AWS for a Recommendation System

**About This Project:** An end-to-end data pipeline I engineered on AWS, demonstrating the integration of batch (Glue, S3) and real-time streaming (Kinesis, Lambda, Firehose) processing to feed a recommendation system. This project showcases infrastructure automation with Terraform and the practical application of cloud services for scalable data ingestion, transformation, and storage, including vector embeddings for recommendations.

---

This repository details an advanced data pipeline I designed and implemented on Amazon Web Services (AWS) to power a recommendation system. The solution robustly handles both **batch data processing** (for historical data and model training inputs like embeddings) and **real-time streaming data** (for user activity), showcasing a modern hybrid architecture. My focus was on leveraging serverless and managed AWS services for scalability, automating infrastructure deployment with Terraform, and building a system capable of generating timely user recommendations.

## My Role & Key Achievements:

As the sole engineer for this project, I was responsible for the complete lifecycle, from architectural design to implementation and deployment. Key achievements and skills I applied include:

* **Hybrid Data Pipeline Architecture:**
    * Designed and implemented a comprehensive solution integrating separate batch and streaming pathways to process different data velocities and types.
* **Batch Processing Implementation (AWS Glue & S3):**
    * Developed an **AWS Glue job** (Python/PySpark script) for ETL operations on historical batch data, including the creation of embeddings (e.g., for items or users) necessary for the recommendation model.
    * Utilized **Amazon S3** for staging raw batch data and storing processed outputs, including embeddings destined for a vector database.
* **Real-Time Streaming Pipeline Implementation (AWS Kinesis & Lambda):**
    * Configured **AWS Kinesis Data Streams** to ingest real-time user activity events (e.g., clicks, views).
    * Developed an **AWS Lambda function** (Python) to process incoming stream data, apply a recommendation model (simulated or actual), and transform events into user-specific recommendations.
    * Used **AWS Kinesis Data Firehose** to reliably deliver the transformed, real-time recommendations from Lambda to an **Amazon S3** bucket for consumption or further processing.
* **Infrastructure as Code (IaC) with Terraform:**
    * Authored **Terraform configurations** to automate the provisioning and management of all AWS resources, including Kinesis streams, Firehose delivery streams, Lambda functions, IAM roles, S3 buckets, and Glue jobs.
* **Scalable & Serverless Design:**
    * Leveraged managed and serverless AWS services (Kinesis, Lambda, Glue, S3) to build a pipeline that can scale with data volume and processing needs.
* **Data Engineering for Recommendation Systems:**
    * Demonstrated understanding of the data requirements for a recommendation system, including processing historical data for model inputs (embeddings) and handling real-time user interactions for dynamic recommendations.

## Pipeline Architecture Overview:

I designed the system with two distinct yet complementary data flows:

1.  **Batch Pipeline:**
    * **Source:** Historical data (e.g., user-item interactions, item metadata) stored in Amazon S3.
    * **Processing:** An AWS Glue ETL job processes this data, potentially generating user/item embeddings or other features for the recommendation model.
    * **Storage:** Processed features and embeddings are stored, for example, in a vector database (conceptual in this project, could be RDS with pgvector, OpenSearch, etc.) or S3.

    ![Batch Pipeline Architecture](./docs/de-c1w4-diagram-batch.drawio.png)

2.  **Streaming Pipeline:**
    * **Source:** Real-time user activity (e.g., product views, clicks, purchases) is ingested into an AWS Kinesis Data Stream.
    * **Processing:** An AWS Lambda function consumes data from the Kinesis stream. It applies transformation logic, which could involve invoking a recommendation model (using pre-calculated embeddings from the batch pipeline) to generate personalized recommendations.
    * **Delivery:** AWS Kinesis Data Firehose takes the output from Lambda (recommendations) and delivers it to a designated Amazon S3 bucket in near real-time.

    ![Streaming Pipeline Architecture](./docs/de-c1w4-diagram-stream.drawio.png)

## Technologies Leveraged:

* **Cloud Platform:** Amazon Web Services (AWS)
* **Batch Processing:** AWS Glue (for ETL), Amazon S3 (for data storage)
* **Stream Processing:** AWS Kinesis Data Streams (ingestion), AWS Lambda (transformation/recommendation generation), AWS Kinesis Data Firehose (delivery)
* **Infrastructure as Code:** Terraform
* **Programming Language:** Python (for Glue jobs and Lambda functions)
* **Data Formats:** JSON, Parquet (as applicable for Glue/S3)

## Project Structure Highlights:

* `terraform/`: Contains all Terraform configuration files (`main.tf`, `variables.tf`, `outputs.tf`) for deploying the AWS infrastructure.
* `lambda/`: Houses the Python code for the AWS Lambda function (`transformation_function.py`) used in the streaming pipeline.
* `scripts/`: Includes the Python/PySpark script for the AWS Glue job (`glue_job.py`) used in the batch pipeline.
* `docs/`: Contains architecture diagrams (`de-c1w4-diagram-batch.drawio.png`, `de-c1w4-diagram-stream.drawio.png`) and other documentation.

## Setup & Deployment:

1.  **Prerequisites:** AWS Account, Terraform installed, Python 3.x, AWS CLI configured.
2.  **Clone Repository.**
3.  **Configure AWS Credentials:** Ensure your AWS CLI is configured with permissions for Kinesis, Firehose, S3, Lambda, and Glue.
4.  **Initialize & Apply Terraform:**
    ```bash
    cd terraform
    terraform init
    terraform apply
    ```
    (Confirm the deployment when prompted).
5.  **Verification:** Monitor CloudWatch logs for Lambda and Glue job status. Check S3 buckets for ingested batch data and real-time recommendation outputs.

## Future Enhancements I Would Consider:

* Implement a more sophisticated recommendation model within the Lambda function or via an SageMaker endpoint.
* Integrate the output recommendations with a user-facing application or notification service (e.g., SES, SNS).
* Enhance monitoring and alerting using CloudWatch Alarms and dashboards.
* Incorporate a dedicated vector database for storing and querying embeddings efficiently.
* Add robust data validation and quality checks at various stages of both pipelines (e.g., using Great Expectations or Deequ).

---
