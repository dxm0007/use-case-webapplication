
 
Describe the CI/CD process for the project in terms of workflow diagrams. 
You can provide a general, high-level workflow diagram that illustrates the typical CI/CD process without going into the specific implementation details
We need to create two separate ci/cd process:
1.	Front end (React application)
2.	Backend (Microservices)




Frontend(Angular):
 
1.	Code Checkout
2.	Build using below npm command
  -- NPM install
  -- NPM build
  -- NPM test
3. Quality Check using Sonarqube
4. Get the package created in tgz format and deploy to target server (google play store)
 

Backend (spring boot microservices):

CI flow:
1.	Code Checkout
2.	Build using below maven command
    -- maven clean install 
    -- unit testing
    -- integration testing

3.	Quality Check using Sonarqube
4.	Create package for project

CD Flow:  Since we are going to ECS fargate for backend implementation
1.	 Build App Image (Build Docker container image)
2.	  Upload App Image (Push the docker image to AWS ECR/docker hub)
3.	Deploy to ECS staging/production (Use AWS CLI from Jenkins to deploy the latest image from Amazon ECR/dockerhub and deploy it to Amazon ECS staging Cluster)


