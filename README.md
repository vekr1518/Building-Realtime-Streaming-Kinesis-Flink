# Building-Realtime-Streaming-Kinesis-Flink

## Use Case Depicted in this project:

This Project will simulate real-time accident data and architect a pipeline to help us analyze and take quick actions using AWS Kinesis, Apache Flink, Grafana, and Amazon SNS. The services used in this project are highly scalable, on-demand, and cost-effective.

This Project uses the [US accidents dataset](https://www.kaggle.com/datasets/sobhanmoosavi/us-accidents), which includes a few of the following fields: 
- Severity
- Start_Time
- End_Time
- Location
- Description
- City
- Country


# Goal of this project is to have three endpoints:
- **A Raw layer** - Raw data is streamed directly and serves as the single source of truth (SSOT).
- **Analytical layer** - This layer stores the filtered and transformed raw data using Apache Flink into the lakehouse for future reporting, BI applications,  and developing data science applications on
top of it.
- **Real-time layer** - The layer serves the cases over a specific severity threshold and is reported via a Grafana Dashboard.  Alerts can be created easily in Grafana with the help of metrics and the graphs formed. Notifications are sent quickly to the concerned departments in this layer.

# Tech Stack:
## Languages
- SQL, Python3
## Services 
- AWS S3, 
- AWS Glue, 
- AWS Athena, 
- AWS Cloud9, 
- Apache Flink, 
- Amazon Kinesis,
- Amazon SNS, 
- AWS Lambda, 
- Amazon CloudWatch, 
- Grafana, 
- Apache Zepplin

# Architecture
![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](https://github.com/vekr1518/Building-Realtime-Streaming-Kinesis-Flink/blob/main/Architecture.png)

# Implementation Steps:
1. Create an S3 bucket
2. Upload [US accidents dataset](https://www.kaggle.com/datasets/sobhanmoosavi/us-accidents) in S3 through aws cli or interface
3. Creat two Datastream in Kinesis Datastream. One for raw data capture and another one for processed/aggregated data
4. Setup Cloud9 environment and run the [Simulation Code](https://github.com/vekr1518/Building-Realtime-Streaming-Kinesis-Flink/blob/main/Stream-data-app-simulation.py)
    - Read the file from s3
    - Convert each row to JSON
    - Add a Transaction Timestamp (Txn_Timestamp)
    - Push each data to datastream created
5. Create a Flink Streaming Application
6. Execute the code [SQL Code](https://github.com/vekr1518/Building-Realtime-Streaming-Kinesis-Flink/blob/main/sql-flink-us-accidents-Zeppelin.rtf)
    - This code will create tables in the database and insert records
7. Build and deploy the Flink application in Kinesis Data Analytics (KDA)
8. Execute the [Lambda Function](https://github.com/vekr1518/Building-Realtime-Streaming-Kinesis-Flink/blob/main/lambda_function.py)
    - Lamba function reads data from data stream, execute the data and publish in cloudwatch
    - SNS alert also configured in Lambda function
9. Create CloudWatch Metrics
10. Create Grafana Dashboards for visualizing the data
11. Create Kinesis Firehose and read the data from datastream and store it in s3 (**NOTE:** This step is required for data retention. KDA is the main player for processing the data. if KDA fails due to unforeseen reasons, data will be lost as the Kinesis Data Stream will keep the data for 1 day only. To avoid this SPOF, We are creating a Kinesis Firehose to process and save the data back to S3)

## Grafana Dashboard:
![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](https://github.com/vekr1518/Building-Realtime-Streaming-Kinesis-Flink/blob/main/Grafana_Dashboard.png)



