#Deploy-the-Web-Application-in-AWS-Kubernetes
This project demonstrates the deployment of a web application on Amazon Web Services (AWS) using Kubernetes (EKS), providing a highly scalable and efficient solution for managing production-grade applications."Task 1(Video link): https://drive.google.com/file/d/1upt9JdKhtANaopiIS5CfKIcqiwQ27vqN/view?usp=sharing
DEPLOY A WEB APPLICATION IN AWS/KUBERNETES

Step 1:- Launch a New EC2 Instance (Amazon Linux - t2.micro)

• Go to the AWS Management Console and launch a new EC2 instance.
• Choose "Amazon Linux 2 AMI" as the operating system.
• Select an instance type (t2.micro is a good choice for testing purposes and free tier).
• Create new key pair and download it.Configure security groups, allowing SSH (port 22) and HTTP (port 80).
• Launch the instance and connect to it via SSH (In MobaXterm Tool).
![1](https://github.com/user-attachments/assets/3d4c2fe7-1938-4120-8448-736ec352d570)
Step 2:- Install kubectl (Kubernetes CLI)

• After connecting to the EC2 instance, run the following commands to install kubectl:
--"curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.30.0/2024-05-12/bin/linux/amd64/kubectl
sudo mv ./kubectl /usr/local/bin
chmod +x ./kubectl
kubectl version"
• This will download kubectl, move it to /usr/local/bin for execution, apply the necessary permissions, and verify the version.
![2](https://github.com/user-attachments/assets/e82f1cc7-6c4f-46f6-a9e5-a3737a318899)
Step 3:- Install AWS CLI

• Install the AWS Command Line Interface (CLI) using these commands:
--"curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
aws --version"
• This installs the latest version of the AWS CLI and verifies the installation.
![3](https://github.com/user-attachments/assets/f3e49ca0-39ec-4e10-b030-e73b1f154b8e)
Step 4:- Install eksctl (EKS Cluster Management Tool)

• To simplify EKS cluster creation, install eksctl:
--"curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version"
• This command downloads and installs eksctl, a command-line tool for managing EKS clusters.
![5](https://github.com/user-attachments/assets/2a0f73f2-af93-43ba-a4aa-47a70c2c3ad4)
Step 5:- Create a New IAM Role

• Go to the IAM section in the AWS Console and create a new role with the following permissions:
o IAM FullAccess – We need create all these roles individually (or) otherwise we give one role is “AdministratorAccess” (VPC FullAccess,EC2 FullAccess,CloudFormation FullAccess).
![6](https://github.com/user-attachments/assets/85a42a0b-a6fd-44cd-a0a0-0852f5364312)
Step 6:- Attach IAM Role to the EC2 Instance

• Attach the created role to the EC2 instance used as the management host. This allows the instance to interact with other AWS services.
![7](https://github.com/user-attachments/assets/6876cf82-a2cb-4a27-929c-f8014894327e)
Step 7:- Create EKS Cluster using eksctl

• To create the EKS cluster, use the eksctl command.
--Mumbai (ap-south-1):
"eksctl create cluster --name demo-cluster --region ap-south-1 --node-type t2.micro --zones ap-south-1a,ap-south-1b" • This will create a new EKS cluster in the specified region, using the specified instance type and zones.
![8](https://github.com/user-attachments/assets/2485e33f-ec28-4c73-aeb9-57432e530f6e)
![9](https://github.com/user-attachments/assets/482fe326-91b6-4f9e-9af2-75157ddeb5c9)
Step 8:- Deploy Web-httpd Pods on Kubernetes

• Create a Deployment for web-httpd: To deploy an given demo-web-httpd application with 1 replicas:
--"kubectl create deployment demo--web-httpd --image=ss1927/httpd --replicas=1 --port=80"
• Check the Status:
List all resources - "kubectl get all"
List the running pods - "kubectl get pods"
• After all this,To run the webapp with help this command:
--"Kubectl run webapp –image=ss1927/httpd"
![9](https://github.com/user-attachments/assets/a9d428be-a79b-434f-b7da-d9b6c5e79bc6)
Step 9:- Expose the Deployment as a Service

• To expose the Nginx deployment via a LoadBalancer, follow these steps:
--Expose the Deployment: "kubectl expose deployment demo--web-httpd --port=80 --type=LoadBalancer"--Check the Service: To see the service details and external IP (LoadBalancer IP) "kubectl get services -o wide"

![10](https://github.com/user-attachments/assets/9ec6cece-f457-4d33-ae2b-4aa61f60b032)
![12](https://github.com/user-attachments/assets/89c0ce1a-8d37-4b8a-9e62-3031c6f1168c)

Step 10:-Output 
![11](https://github.com/user-attachments/assets/c5a0aec2-526f-4d09-8841-6155796763ec)
![photo_2024-12-12_21-03-09](https://github.com/user-attachments/assets/4d2dd1ce-fe2e-426c-acae-3602c87d3b0c)
![photo_2024-12-12_21-03-11](https://github.com/user-attachments/assets/1291b657-2eb2-4b44-8135-312b479772e9)
![photo_2024-12-12_21-03-13](https://github.com/user-attachments/assets/4e03b8fe-c8f9-42b8-a5a4-d37a204ff7ea)
![photo_2024-12-12_21-03-14](https://github.com/user-attachments/assets/83c77713-8222-4e56-93c8-bb277192ddca)
![photo_2024-12-12_21-03-15](https://github.com/user-attachments/assets/b57f7511-290f-4606-aa11-86287f98a12a)
Conclusion:
Deploying a web application on AWS using Kubernetes (EKS) offers a scalable and efficient solution. By leveraging EC2, EKS, and Kubernetes tools like kubectl and eksctl, the deployment process is streamlined. Integrating Auto Scaling ensures high availability and performance, while Kubernetes simplifies container management. This approach enhances flexibility and scalability, making it an ideal choice for modern cloud environments. Overall, AWS and Kubernetes together provide a robust platform for deploying and managing applications in production.
