
# Part: B – System Architecture
## Overview
For an existing e-commerce application, I've come up with a plan to make it better. The new design is scalable, cost effective, performs well, and has built-in logging and monitoring. This means we can quickly spot and fix any issues, thanks to better management tools.
## Current Architecture
The current architecture involves users accessing the application by hitting the DNS, which resolves to the IP address of the web server. The web server, in turn, is connected to a database and an object storage bucket.
![Current Architecture](https://github.com/Zunaied/Devops-task-v2/blob/main/Existing%20Architecture.png)

## Solution Description
To solve this i have used aws cloud. Aws has every service and it is most user firendly cloud globaly.

![Solution Architecture](https://github.com/Zunaied/Devops-task-v2/blob/main/E-commerce%20Architecture.png)

In this solution, various components are used to improve performance, reduce costs, and enable scalability.

- Initially, the user interacts with the **DNS to resolve the IP**, and then the request is directed to the **web server** or **AWS CloudFront**. 
- In this architecture, we include **CloudFront edge location** after the DNS. If a user requests data that is not present in the **edge location**, it redirects to the **origin server**, fetches the response, and is then **cached in the edge location** for subsequent requests. CloudFront is utilized to efficiently serve e-commerce traffic globally.

- User requests go through **CloudFront**, entering the system via the **Internet Gateway** into the **VPC**. Inside the VPC, a **Load Balancer** directs the requests to the web server.

- Servers are configured with **auto scaling** to dynamically adjust to varying traffic. It scales up during peak hours to handle high demand and scales down during lighter traffic periods, ensuring optimal resource utilization.

- The application uses a database with a **master write instance** for writing and **Read Replicas** for reading data. Utilizing a single availability zone (AZ) for cost-effectiveness, read replicas are employed, benefiting from their no-cost feature in a single AZ Read Replica database setup. It quantity limitation for read replica.

- To manage various read and write APIs, along with background jobs, we implemented an efficient solution using **API Gateway** as an event trigger for **Lambda Functions**. This serverless approach ensures minimal operational costs.
 
- To handle external queries for product lists, we integrated **API Gateway** and **Lambda Function**. The external queries are efficiently processed from the S3 bucket.

- We've also added a **logging and monitoring section** for a more reliable setup. However, you can skip this part to save costs since **SNS** charges for alerts, whereas **CloudWatch** is free. **CloudWatch** lets you keep an eye on server metrics like CPU usage. It also tracks logs for auditing. If anything goes wrong, **SNS** sends alerts for a quick response.









