## Add IAM oidc connector

```bash
eksctl utils associate-iam-oidc-provider --cluster demo-cluster --approve
```

## Install and create IAM Policy

```bash
curl -O https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.11.0/docs/install/iam_policy.json

aws iam create-policy \
--policy-name AWSLoadBalancerControllerIAMPolicy \
--policy-document file://iam_policy.json
```

## Create IAM role

``` bash
eksctl create iamserviceaccount \
--cluster=demo-cluster \
--namespace=kube-system \
--name=aws-load-balancer-controller \
--role-name AmazonEKSLoadBalancerControllerRole \
--attach-policy-arn=arn:aws:iam::<YOUR_AWS_ACCOUNT_ID>:policy/AWSLoadBalancerControllerIAMPolicy \
--approve
```

## Install AWS Load Balancer Controller with Helm

```bash
helm repo add eks https://aws.github.io/eks-charts
```
```bash
helm repo update
```
```bash
helm install aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system \
--set clusterName=demo-cluster \
--set serviceAccount.create=false \
--set serviceAccount.name=aws-load-balancer-controller \
--set region=us-east-1 \
--set vpcId=<YOUR_VPC_ID>
```