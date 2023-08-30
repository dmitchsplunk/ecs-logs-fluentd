# ecs-logs-fluentd

This example shows how to deploy the Splunk OpenTelemetry collector as a task definition in ECS using EC2 instances. This task definition should run as a daemon service in ECS. 

It then shows how to deploy a task definition including an nginx container, that collects logs using a Fluent Bit sidecar container. This task definition should run as a replica in ECS. 

The logs are then forwarded to the Fluent Forward receiver configured on port 8006 in the OpenTelemetry collector.  

The "host" network mode is used for both task defintions, to allow the nginx task definition to connect to the OpenTelemetry collector. 

If the "awsvpc" network mode is required instead, then the OpenTelemetry collector should be installed as a sidecar container within the same task definition as the nginx container.

Installation Steps: 

1. [Launch a new ECS Cluster with EC2] (https://docs.aws.amazon.com/AmazonECS/latest/developerguide/create-ec2-cluster-console-v2.html) 

2. Create ECS Task Definition for Splunk OTel Collector

Use the splunk-otel-collector-task-definition.json file to create a new task definition. Ensure the SPLUNK_REALM and SPLUNK_ACCESS_TOKEN environment variables are set correctly for your environment. 

3. [Create ECS Service for Splunk OTel Collector] (https://github.com/signalfx/splunk-otel-collector/tree/main/deployments/ecs/ec2#launch-the-collector)

Ensure that the Launch Type is EC2, and that the Service Type is Daemon. 

4. Confirm that Infrastructure Data is Flowing into Splunk Observability Cloud

5. Create Nginx Task

Use the nginx-task-definition.json file to create a new task definition.

6. Create Nginx Service

Ensure that the Launch Type is EC2, and that the Service Type is Replica. 
