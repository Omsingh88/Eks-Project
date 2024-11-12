# Eks-Project
Commands 

1. Create a cluster on EKS. Depending on your internet speed, the cluster will take 10–15 minutes to connect.

eksctl create cluster --name demo-cluster --region us-east-1 --fargate

2. Update Kubeconfig on your EKS cluster.

aws eks update-kubeconfig --name demo-cluster --region us-east-1

3 .create the EKS Fargate profile.

eksctl create fargateprofile \
  --cluster demo-cluster \
  --region us-east-1 \
  --name fargate-profile \
  --namespace game-2048

4 .Deploy the 2048 Game Application:

kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.5.4/docs/examples/2048/2048_full.yaml

5. Next, you have to create and configure an IAM OIDC provider for your demo-cluster.

eksctl utils associate-iam-oidc-provider --cluster $cluster_name --approve

6. Setup for ALB controller add on.
curl -O https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.5.4/docs/install/iam_policy.json

7. Finally, We’ll Deploy AWS Load Balancer Controller:
helm repo add eks https://aws.github.io/eks-charts
