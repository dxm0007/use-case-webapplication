Draw the architecture diagram based on the functional requirements and what AWS services are you going to use and why?
You can sketch a high-level architecture diagram that showcases the key AWS services
and components, without delving into the specifics of how they will be implemented.
 Below is the AWS component to be used for implementing the requurement.
1. Virtual Private Cloud (VPC) - used to provision resources with a virtual private network to provide greater control over access and security of resources. It has below components alonwith its use:
 > Private subnets - to block internet access
 > Public subnets - allows internet access
 > Security groups - allows us to provide connections between resources in the VPC, e.g. allow the load balancer to access Fargate containers 

2. ECS Cluster(Fargate):It is being used for hosting the containerized services. Amazon ECS is a highly scalable and high-performance container orchestrator. For solution of case stidy, the Fargate launch type is used, so that containers are launched on the Fargate serverless compute engine, and we don’t have to provision or manage any EC2 instances. In this service auto scaling is also enabled, so that the number of containers in each service can scale up and down automatically based on % CPU usage. Containers will be launched across multiple Availability Zones in the AWS Region, to get high availability.
A Service responsible for deploying ECS tasks (with autoscaling based on resources)
Fargate task definitions to store the configuration for spinning up ECS containers and defines the amount of resource each task can use.
An IAM role assumed by the containers to give role-based access to other AWS resources


3. Application Load Balancer:
Application Load Balancer (ALB) works with ECS Fargate to efficiently distribute incoming traffic to our containerized applications. It helps direct users to the right service within our application, ensures only healthy services receive traffic, and supports smooth scaling and updates. ALB also manages secure connections, making it easier to handle web traffic in our deployments.


4. Cloudfront with WAF : CloudFront, combined with AWS WAF (Web Application Firewall), provides a powerful security and content delivery solution for ECS clusters. CloudFront serves as a global content delivery network (CDN) that caches and delivers your application content from edge locations, reducing latency and improving user experience. AWS WAF protects your application by filtering and blocking malicious traffic, such as SQL injections and cross-site scripting (XSS) attacks.It is being used for caching and extra security.

5. Route53 and Certificate manager for creating a nice SSL domain


6. API Gateway : API Gateway acts as a front door for accessing your ECS services, enabling secure and scalable communication between clients and your containerized applications. It handles all the incoming API requests, routing them to the appropriate ECS service, managing traffic, and providing features like rate limiting, authentication, and monitoring. API Gateway simplifies the process of exposing your ECS services to the outside world, ensuring that your APIs are secure and well-managed.
                  As Amazon ECS services are private resources in a Virtual Private Cloud (VPC), API Gateway uses a VPC link to connect to them in a private way. A VPC link is a set of elastic network interfaces in the VPC, assigned to and managed by API Gateway, so that API Gateway can talk privately with other resources in the VPC. This way, Amazon ECS services can be launched in private subnets and don’t need a public IP. 

7. Amazon DynamoDB: DynamoDB is a managed NoSQL database that integrates seamlessly with ECS clusters. It provides scalable and high-performance storage for application data, offering low-latency access. When used with ECS, DynamoDB handles data storage without requiring server management, scaling automatically based on demand. This setup simplifies data management, improves application performance, and ensures high availability, allowing our ECS services to efficiently access and manage data.It is used for persisting the data. It is a key-value and document database that provides single-millisecond performance at any scale. 



