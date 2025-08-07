# 2048 Game: Serverless K8s on AWS EKS

A production-ready deployment of the 2048 game using AWS EKS Fargate and ALB Ingress, demonstrating modern cloud-native architecture.

## 🏗️ Architecture & Traffic Flow
```
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│                     User (example.com)                          │
│                            │                                    │
│                            ▼                                    │
│                     Internet Traffic                            │
│                            │                                    │
│                            ▼                                    │
│              Application Load Balancer (ALB)                    │
│                            │                                    │
│         [Configured by AWS ALB Ingress Controller]              │
│          - Provisions ALB automatically                         │
│          - Sets up listeners and target groups                  │
│                            │                                    │
│                            ▼                                    │
│                     Ingress Resource                            │
│         [Defines routing rules for example.com]                 │
│                            │                                    │
│                            ▼                                    │
│                    Kubernetes Service                           │
│            [ClusterIP/NodePort -> Routes to Pods]               │
│                            │                                    │
│                            ▼                                    │
│                AWS EKS Cluster (Fargate)                        │
│                            │                                    │
│                            ▼                                    │
│                      2048 Game Pod                              │
│         [Processes requests and returns responses]              │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```


## 🛠️ Tech Used
- AWS EKS (Elastic Kubernetes Service)
- AWS Fargate
- AWS ALB Ingress Controller
- Kubernetes
- Helm

## 🚀 Features
- Fully managed Kubernetes cluster on AWS EKS
- Fargate profile for serverless pod execution
- ALB Ingress Controller for external access
- Helm-based deployment

## 📦 Prerequisites
Install the following tools locally:
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [eksctl](https://eksctl.io/)
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)
- [Helm](https://helm.sh/docs/intro/install/)

Configure AWS CLI:
```bash
aws configure
```
This will prompt you for your AWS Access Key ID, Secret Access Key, region, and output format. Credentials are saved in ~/.aws/credentials (Linux/Mac) or %USERPROFILE%\.aws\credentials (Windows).

## 🚀 Setup Process
The setup process is divided into several steps, with detailed commands available in the respective files:

1. Configure AWS CLI (`01_configure_aws.md`)
2. Create EKS Cluster (`02_create_cluster.md`)
3. Deploy Application (`03_deploy_app.md`)
4. Setup ALB Controller (`04_setup_alb_controller.md`)
5. Verify Deployment (`05_verify_deployment.md`)

## 🔧 Troubleshooting
Common issues and solutions:

1. Pods not starting:
   - Check Fargate profile configuration
   - Verify namespace labels

2. ALB not provisioning:
   - Verify IAM roles and policies
   - Check VPC subnet tags

3. Game not accessible:
   - Confirm security group settings
   - Verify ingress configuration