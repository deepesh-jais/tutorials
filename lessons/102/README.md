# How to Create EKS Cluster Using Terraform

[YouTube Tutorial]()


aws eks --region us-east-1 update-kubeconfig --name demo

kubectl get endpoints


Prerequisites
- An existing IAM OIDC provider for your cluster.
- Node groups with Auto Scaling groups tags. you must manually tag your Auto Scaling groups with the following tags.

k8s.io/cluster-autoscaler/<cluster-name> : owned
k8s.io/cluster-autoscaler/enabled : TRUE

Create an IAM policy and role
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "autoscaling:DescribeAutoScalingGroups",
                "autoscaling:DescribeAutoScalingInstances",
                "autoscaling:DescribeLaunchConfigurations",
                "autoscaling:DescribeTags",
                "autoscaling:SetDesiredCapacity",
                "autoscaling:TerminateInstanceInAutoScalingGroup",
                "ec2:DescribeLaunchTemplateVersions"
            ],
            "Resource": "*",
            "Effect": "Allow"
        }
    ]
}
```

curl -o cluster-autoscaler-autodiscover.yaml https://raw.githubusercontent.com/kubernetes/autoscaler/master/cluster-autoscaler/cloudprovider/aws/examples/cluster-autoscaler-autodiscover.yaml

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/eks_cluster



kubectl exec aws-cli -- aws s3api list-buckets