# Cloud DevOps Engineer Capstone Project

This project represents the successful completion of the last final Capstone project and the Cloud DevOps Engineer Nanodegree at Udacity.

## What did I learn?

 1. Linting project codes.
 2. Docker for containerize the applicaion.
 3. Deploy containerize application using Docker and prediction.
 4. Configure Kubernetes and create a Kubernetes cluster
 5. Deploy container using and prediction.
 6. Installation of Kubernetes and Minikube.

## Application

The Application is render a simple webpage in the user's browser.
A requirements.txt is used to ensure that all needed dependencies come along with the Application.

## Kubernetes Cluster

I used AWS CloudFormation to deploy the Kubernetes Cluster.
The CloudFormation Deployment can be broken down into four Parts:
- **Networking**, to ensure new nodes can communicate with the Cluster
- **Elastic Kubernetes Service (EKS)** is used to create a Kubernetes Cluster
- **NodeGroup**, each NodeGroup has a set of rules to define how instances are operated and created for the EKS-Cluster
- **Management** is needed to configure and manage the Cluster and its deployments and services. I created two management hosts for extra redundancy if one of them fails.

#### List of deployed Stacks:
![Cloud Formation Stacks](image.png)

#### List of deployed Instances:
![EC2 instance](image-1.png)

## CircleCi - CI/CD Pipelines

I used CircleCi to create a CI/CD Pipeline to test and deploy changes manually before they get deployed automatically to the Cluster using Ansible.

#### From Zero to Hero demonstration:

![Circleci Pipeline](image-2.png)

## Linting using Pylint and Hadolint

Linting is used to check if the Application and Dockerfile is syntactically correct.
This process makes sure that the code quality is always as good as possible.

#### This is the output when the step fails:

![Lint Fail](screenshots/lint-fail.png)


#### This is the output when the step passes:

![Lint Pass](screenshots/lint-pass.png)

## Access the Application

After the EKS-Cluster has been successfully configured using Ansible within the CI/CD Pipeline, I checked the deployment and service as follows:

```
kubectl get deployments
NAME                          READY   UP-TO-DATE   AVAILABLE   AGE
capstone-project-deployment   4/4     4            4           105m

kubectl get services
NAME                       TYPE           CLUSTER-IP      EXTERNAL-IP                                                              PORT(S)        AGE
capstone-project-service   LoadBalancer   10.100.107.25   a4261669700ee4272a28a1354c6aa12c-900751887.us-east-1.elb.amazonaws.com   80:30282/TCP   105m
kubernetes                 ClusterIP      10.100.0.1      <none>                                                                   443/TCP        113m                                                                      443/TCP        80m
```

Public LB DNS: http://a4261669700ee4272a28a1354c6aa12c-900751887.us-east-1.elb.amazonaws.com/