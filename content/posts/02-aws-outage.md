---
author: "Jithin Zachariah"
title: "AWS Kinesis Outage"
date: "2021-01-02"
ShowToc: true
---

### Outage

Several AWS offerings based on the Northern Virginia (US-EAST-1) Region experienced service disruption on November 25th. It took almost 12 hours for all the affected services to come back up and operate normally.

### Root Cause

AWS Kinesis is a Managed offering from AWS compared to Apache Kafka. Kinesis is used for application logs, monitoring streaming, real-time big data processing, etc. Architecturally Kinesis can be broken down into the backend cluster and the frontend fleet.

- **Backend Cluster**
  - Processes a stream of data.
  - Owns many shards.
  - Provides consistent scaling and fault isolation.

- **Frontend Fleet**
  - Handles authentication, throttling, and request routing to backend shards.
  - Each server maintains a cached data structure called **shard-map**.
    - Used to route requests to the correct backend shards.

- **Peer-to-Peer Communication**
  - Each frontend server communicates with others using a process-driven model (like Apache).
  - Involves one or more threads for server-to-server communication.
  - Example: In a fleet of 10 servers, each server uses at least 9 threads to talk to the rest.

AWS Kinesis along with other AWS offerings like Amazon Cognito, CloudWatch, EventBridge, Service Health Dashboard, EKS that used AWS kinesis underneath were affected due to this outage.
The Root Cause

As per the technical statement released by AWS, the issues occurred after a scheduled capacity addition to the AWS Kinesis frontend clusters on November 25th.

The addition of the new capacity(server) to the frontend fleet caused all of the servers in the fleet to exceed the maximum number of threads(used for peer-peer communicaton) allowed by the underlying operating system configuration. As this limit was being exceeded, cache construction was failing to complete and frontend servers were ending up with corrupted shard-maps that left them unable to route requests to backend clusters.

### Conclusion
Several services use Kinesis underneath which caused a greater impact for the outage, However AWS engineers managed to work under pressure and could restore all the services. Hats off to the entire team. Further AWS has mentioned they’ll improve their Kinesis architecture for better scalability and performance. The full technical statement is available at https://aws.amazon.com/message/11201/