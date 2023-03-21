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
- A Raw layer - Raw data is streamed directly and serves as the single source of truth (SSOT).
- Analytical layer - This layer stores the filtered and transformed raw data using Apache Flink into the lakehouse for future reporting, BI applications,  and developing data science applications on
top of it.
- Real-time layer - The layer serves the cases over a specific severity threshold and is reported via a Grafana Dashboard.  Alerts can be created easily in Grafana with the help of metrics and the graphs formed. Notifications are sent quickly to the concerned departments in this layer.

# Tech Stack:
## Languages
- SQL, Python3
## Services 
- AWS S3, AWS Glue, AWS Athena, AWS Cloud9, Apache Flink, Amazon Kinesis,Amazon SNS, AWS Lambda, Amazon CloudWatch, Grafana, Apache Zepplin

# Architecture
![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](https://github.com/vekr1518/Building-Realtime-Streaming-Kinesis-Flink/blob/main/Architecture.png)

