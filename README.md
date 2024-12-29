# Real-time Data Management on AWS Cloud for TELEMAX

This project implements a real-time data management solution on AWS for TELEMAX, a company building networks in rapidly growing markets. The solution addresses the need for a NoSQL-based data warehousing system that can handle real-time data ingestion and analysis for continuous topology optimization.

## Architecture

The architecture consists of the following AWS services:

* **Kinesis Stream:** Ingests real-time networking data.
* **DynamoDB Table (TELEMAX):** Stores the ingested data with `hardwareID` as the partition key and `Timestamp` as a sort key. Additional attributes (`Data1`, `Data2`, `Data3`) store domain-specific information.
* **Lambda Function:** Processes data from the Kinesis stream and writes it to the DynamoDB table.
* **EC2 Instance with Kinesis Agent:**  Simulates real-world data generation and sends it to the Kinesis stream.
* **IAM Roles:**  Provide least-privilege access to the Lambda function and EC2 instance.


## Implementation Details

1. **Kinesis Stream:** A Kinesis data stream with 2 shards is created. Sharding improves stream performance and scalability.

2. **DynamoDB Table:** A DynamoDB table named `TELEMAX` is created with the specified partition and sort keys, along with additional attributes.

3. **IAM Role:** An IAM role with `KinesisFullAccess`, `putRecord`, and `putRecords` permissions is created and assigned to the Lambda function.  The EC2 instance also has an IAM role with `KinesisFullAccess`.

4. **Lambda Function:** A Python 3.9 Lambda function is created. It reads data from the Kinesis stream and writes it to the DynamoDB table.

5. **EC2 Instance and Kinesis Agent:** An Amazon Linux EC2 instance is launched. The Kinesis Agent is installed and configured to send synthetic data from `/tmp/app.log` to the Kinesis stream.  The `agent.json` file is updated with the stream name.

## Results

The solution successfully ingests data into the DynamoDB table. TELEMAX can now leverage this infrastructure to store and analyze their networking data in real-time, enabling continuous topology optimization and other advanced analytics.

## Future Considerations

* **Data Analysis and Visualization:** Implement tools and techniques to analyze and visualize the data stored in DynamoDB.
* **Scaling and Performance:** Monitor and adjust the number of shards in the Kinesis stream and the read/write capacity units of the DynamoDB table based on data volume and performance requirements.
* **Security Hardening:** Implement additional security measures such as encryption at rest and in transit.
* **Alerting and Monitoring:** Set up alerts and monitoring to proactively identify and address any issues with the system.


This setup allows for efficient, scalable, and real-time data management on AWS. It provides a foundation for TELEMAX to leverage the power of real-time data processing for enhanced decision-making and optimized network performance.
