---
title: "Cleanup"
date: 2021-05-11T13:38:18+08:00
weight: 100
draft: false
---

For more hands-on experience, see the dedicated [EMR on EKS Workshop](https://emr-on-eks.workshop.aws/).
#### Empty and delete S3 buckets

```sh
aws s3 rm $s3DemoBucket --recursive
aws s3 rb $s3DemoBucket --force

```

#### Delete IAM Role and policy

```sh
aws iam delete-role-policy --role-name EMRContainers-JobExecutionRole --policy-name EMR-Containers-Job-Execution
aws iam delete-role --role-name EMRContainers-JobExecutionRole

```


#### Delete Virtual Cluster

```sh
aws emr-containers delete-virtual-cluster --id ${VIRTUAL_CLUSTER_ID}

```

To delete the namespace, the node group and the Fargate profile created by this module, run the following commands

```sh
kubectl delete namespace spark

eksctl delete nodegroup --cluster=eksworkshop-eksctl --region=${AWS_REGION} --name=emrnodegroup
eksctl delete nodegroup --cluster=eksworkshop-eksctl --region=${AWS_REGION} --name=emrnodegroup-spot
eksctl delete fargateprofile --cluster=eksworkshop-eksctl --name emr --wait

```