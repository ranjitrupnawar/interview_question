# Technical Interview Questions

## System and Network Administration

1. **What is an inode?**
    - An inode is a data structure on a filesystem on Linux and Unix-like systems that stores information about a file or a directory.

2. **What information is available in an inode?**
    - Inode information includes file size, device ID, user ID of the file's owner, group ID, number of links, file access, change and modification time, and pointers to the data blocks.

3. **How do you check CPU utilization?**
    - Use the `top` or `htop` command to check CPU utilization in real-time.

4. **How can you prioritize processes based on CPU allocation?**
    - Use the `nice` and `renice` commands to set and modify the priority of processes.

5. **I have created a different virtual host for Apache server, but I'm getting a forbidden error. How can I fix this issue?**
    - Ensure the firewall is properly configured to allow traffic to the new virtual host. Also, check and adjust SELinux permissions using `chcon` to set the correct context for the new directory.

6. **How do you enable SELinux for a new virtual host directory?**
    - Use the `semanage fcontext -a -t httpd_sys_content_t '/path/to/new/directory(/.*)?'` command followed by `restorecon -Rv /path/to/new/directory` to apply the new context.

## Scripting and Automation

7. **What is the difference between `grep` and `egrep`?**
    - `grep` is used to search text using basic regular expressions. `egrep` (or `grep -E`) is used for extended regular expressions.

8. **How do you create 10 directories named dir1, dir2, ..., dir10 using a loop in a bash script?**
    ```bash
    #!/bin/bash

    # Loop to create directories
    for ((i = 1; i <= 10; i++)); do
        mkdir "dir$i"
    done
    ```

## Configuration and Deployment

9. **What is the purpose of MCP (Mission Configuration Properties)?**
    - MCPs are used to define configuration settings for a mission-critical application, ensuring consistent behavior across environments.

10. **How do you deploy an application using the source-to-image method with a source in GitHub and a local Docker image using `kubectl`?**
    - Use the `kubectl create deployment <deployment-name> --image=<local-docker-image> --replicas=<number-of-replicas> -- git-repo=<github-repo-url>` command.

## Kubernetes and Docker

11. **What is the difference between a ReplicaSet and autoscaling?**
    - A ReplicaSet ensures a specified number of pod replicas are running at any given time. Autoscaling adjusts the number of pod replicas dynamically based on resource usage or other metrics.

12. **Describe the request flow when accessing an application through an Apache service running in a pod.**
    - The request flows from the user to the Kubernetes service, which routes it to the appropriate pod running the Apache service. Apache then forwards the request to the backend application.

13. **How do you expose a pod in Kubernetes?**
    - Use the `kubectl expose pod <pod-name> --port=<port> --target-port=<target-port> --type=<service-type>` command.

14. **What is the difference between a route and a service in Kubernetes?**
    - A service exposes a set of pods as a network service within the cluster. A route (in OpenShift) exposes a service to external traffic by mapping it to a DNS name.

15. **What is the difference between a Secret and a ConfigMap in Kubernetes?**
    - A Secret is used to store sensitive data such as passwords and tokens. A ConfigMap is used to store non-sensitive configuration data.

16. **How do you check CPU utilization for all physical nodes in a cluster?**
    - Use the `kubectl top nodes` command.

## CI/CD and Build Tools

17. **In a pipeline, what is the "generate pipeline script" option?**
    - This option generates a Jenkins pipeline script based on the chosen configuration options, allowing you to automate the build process.

18. **Describe the Maven lifecycle.**
    - The Maven lifecycle consists of phases such as `validate`, `compile`, `test`, `package`, `verify`, `install`, and `deploy`.

19. **Are you using Artifactory?**
    - Artifactory is a repository manager that supports various package types, including Maven, Docker, and npm, to store and manage binary artifacts.

## Java and Repository Structure

20. **What is the typical folder structure of a Java repository?**
    - A typical Java repository structure includes:
      ```
      src/
          main/
              java/
              resources/
          test/
              java/
              resources/
      pom.xml
      ```

21. **How does your project structure look like? Take one of the backend projects as an example.**
    - The backend project might have the following structure:
      ```
      src/
          main/
              java/
                  com/
                      example/
                          service/
                              Service1.java
                              Service2.java
              resources/
                  application.properties
          test/
              java/
                  com/
                      example/
                          service/
                              Service1Test.java
                              Service2Test.java
              resources/
      pom.xml
      ```

22. **Describe the CI/CD pipeline setup for a service repository.**
    - The CI/CD pipeline for a service repository typically includes:
      - Build pipeline
      - Test pipeline
      - Deployment pipeline

23. **How does the infrastructure pipeline work and what does it contain?**
    - The infrastructure pipeline manages the setup and configuration of infrastructure resources. It includes:
      - Infrastructure as Code (IaC) scripts
      - Configuration management scripts
      - Deployment scripts

24. **How is the infrastructure shared among application components?**
    - Infrastructure is shared through:
      - Common network resources
      - Shared databases
      - Shared storage

25. **What is the repository structure of your application?**
    - The repository structure includes separate repositories for each microservice, common libraries, and infrastructure code.

26. **How many total repositories do you have?**
    - The total number of repositories includes individual service repositories, shared libraries, and infrastructure repositories.

## Microservices and API Management

27. **How do you deploy your microservices and APIs? How do they communicate with each other? How do you maintain security?**
    - Microservices are deployed using Kubernetes. They communicate via internal services and APIs, secured with mutual TLS and API gateways.

28. **Describe the end-to-end process when an end-user accesses your API.**
    - The request goes to the API gateway, which routes it to the appropriate microservice. The backend processes the request and returns a response through the gateway.

## API Deployment and Management

29. **Have you deployed an API?**
    - Yes, APIs are deployed using Kubernetes and exposed via API gateways.

## Terraform and AWS

30. **What modules have you written in Terraform?**
    - Modules for VPC, EC2 instances, RDS, S3, IAM roles, and policies.

31. **How do you onboard new users and grant them access to resources?**
    - New users are onboarded using IAM roles and policies to grant necessary permissions.

32. **How do you manage AWS users?**
    - AWS users are managed through IAM, including user creation, role assignment, and policy management.

## File Transfer and Management

33. **How do you transfer a 1GB file to multiple servers (e.g., 1000 servers)?**
    - Use parallel SCP or rsync with a for loop.

34. **How do you transfer a 1GB file between nodes A, B, and C when A and C are not directly connected?**
    - Transfer the file from A to B, and then from B to C.

## Security and Vulnerability Management

35. **How do you scan your Terraform code for vulnerabilities?**
    - Use tools like TFSec, Checkov, or Terraform Cloud's built-in scanner.

## AWS Networking and Security

36. **What is the difference between a VPC gateway endpoint and a VPC interface endpoint?**
    - Gateway endpoints are for S3 and DynamoDB, while interface endpoints are for other AWS services using PrivateLink.

37. **How can you access your S3 bucket from Account A to Account B?**
    - Use bucket policies and IAM roles to grant cross-account access.

## Disaster Recovery and Cost Management

38. **What are the disaster recovery strategies available in AWS?**
    - Backup and restore, pilot light, warm standby, and multi-site.

39. **How does a low RTO affect the cost of disaster recovery?**
    - Lower RTO typically increases costs due to the need for more active resources and infrastructure.

## Docker and Kubernetes

40. **What is a distroless image?**
    - A distroless image is a minimal Docker image without a package manager or shell, reducing the attack surface.

41. **What is a reverse proxy?**
    - A reverse proxy forwards client requests to backend servers and returns the server's response to the client.

42. **What is `/etc/resolv.conf`?**
    - It is a configuration file for DNS resolver settings on Unix-like systems.

43. **What is a headless service in Kubernetes?**
    - A headless service is a type of service that does not have a cluster IP and is used for service discovery.
