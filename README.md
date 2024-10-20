# End-to-End Batch and Streaming Pipeline with AWS

This repository contains a complete project for building an end-to-end batch and streaming pipeline using AWS services like Kinesis, Firehose, S3, Lambda, Glue, and a vector database. The project demonstrates how to build a recommendation system that processes both batch and real-time streaming data.

## Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Components](#components)
- [Technologies Used](#technologies-used)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [How It Works](#how-it-works)
  - [Batch Pipeline](#batch-pipeline)
  - [Streaming Pipeline](#streaming-pipeline)
- [Deployment Instructions](#deployment-instructions)
- [Future Enhancements](#future-enhancements)
- [License](#license)

## Overview

This project demonstrates the creation of a scalable data pipeline capable of processing both batch and streaming data to generate recommendations for users. The pipeline uses AWS services to automate data ingestion, processing, transformation, and storage.

## Architecture

The pipeline is divided into two main parts:

- **Batch Pipeline**: Using AWS Glue for ETL and S3 for storage.
- **Streaming Pipeline**: Using Kinesis Data Streams, Kinesis Firehose, and Lambda for real-time data processing.

```

## Components

The project is composed of the following components:

1. **AWS Glue**: To process the batch data and store embeddings in a vector database.
2. **AWS Kinesis**: Used to stream real-time user activity.
3. **AWS Lambda**: A transformation function that extracts features and applies the recommender model.
4. **S3 Buckets**: Used to store both the batch data and streaming outputs (recommendations).
5. **Terraform**: Used for infrastructure as code (IaC) to deploy AWS services.

## Technologies Used

- **AWS Glue**
- **AWS Kinesis Data Streams**
- **AWS Kinesis Firehose**
- **AWS Lambda**
- **Amazon S3**
- **Terraform**
- **Python**

## Project Structure

```bash
├── terraform/
│   ├── main.tf                # Main Terraform configuration file
│   ├── outputs.tf             # Terraform output configuration
│   ├── variables.tf           # Terraform variables
├── lambda/
│   └── transformation_function.py # Lambda function for stream transformation
├── docs/
│   └── explanation.md         # Documentation about the project
├── scripts/
│   └── glue_job.py            # AWS Glue job script for batch processing
└── README.md                  # Project readme file
```

## Getting Started

### Prerequisites

- AWS Account
- Terraform installed
- Python 3.x installed
- AWS CLI configured

### Setup Instructions

1. **Clone the repository**:

   ```bash
   git clone https://github.com/yourusername/your-repository.git
   cd your-repository
   ```

2. **Configure AWS credentials**:

   Ensure your AWS CLI is configured with sufficient permissions to create Kinesis, Firehose, S3, and Lambda resources.

3. **Initialize Terraform**:

   Go to the `terraform/` folder and initialize Terraform:

   ```bash
   cd terraform
   terraform init
   ```

4. **Apply Terraform changes**:

   ```bash
   terraform apply
   ```

## How It Works

### Batch Pipeline

1. **Data Ingestion**: AWS Glue extracts data from S3 and processes it to create embeddings.
2. **Storage**: The embeddings are stored in a vector database for later use in the recommendation system.

### Streaming Pipeline

1. **User Activity Stream**: User activities (e.g., clicks, purchases) are captured in real-time using AWS Kinesis Data Streams.
2. **Data Transformation**: AWS Lambda processes the data by applying the recommendation model, transforming the data into user-specific recommendations.
3. **Data Delivery**: Kinesis Firehose delivers the transformed data to the S3 recommendation bucket.

## Deployment Instructions

To deploy the pipeline:

1. Follow the [Setup Instructions](#setup-instructions).
2. Run the Terraform commands to deploy all the necessary infrastructure.
3. Check the S3 bucket for output files and CloudWatch logs to monitor Lambda transformations.

## Future Enhancements

- Add a more advanced recommendation model.
- Integrate with a notification service to send real-time recommendations to users.
- Implement better logging and monitoring for Lambda functions.

## License

This project is licensed under the MIT License.

---

Feel free to customize the content to better fit your project specifics!
