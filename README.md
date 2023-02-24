# Prometheus-Grafana Manifests


## Getting started

```
git clone https://github.com/bharath2602/prometheus-grafana-k8s.git
cd existing_repo
git remote add origin https://github.com/bharath2602/prometheus-grafana-k8s.git
git branch -M main
git push -uf origin main
```

## Notable hints

- Create a new name space for the monitring applications 
- All the monitoring tools are made run as pods in the K8s cluster
- Both the prometheus and grafana needs a configuration file
- All the application needed to be monitored need to expose metrics in '/metric' path any custome path needs to be mentioned in the service annotations

    ```
    prometheus.io/path: "/actuator/prometheus" --> path exposing the metrics
    prometheus.io/port: "8080" --> port exposed in the service
    prometheus.io/scrape: "true" --> for auto-discovery of the service by prometheus
    ```

- Refernce:

    - [Prometheus](https://devopscube.com/setup-prometheus-monitoring-on-kubernetes/)
    - [State-metric](https://devopscube.com/setup-kube-state-metrics/)
    - [Grafana](https://devopscube.com/setup-grafana-kubernetes/)




Sample Bucket configuration
----------------------------
bucket         = <Bucket-Name>
key            = <state-file-path>
region         = <aws-region>
encrypt        = true
kms_key_id     = "alias/terraform-bucket-key"
dynamodb_table = <dynamodb-table-name>
```
- Backend Configurations : [backend](backend/)

- List of Modules :
    
| S.no. | Modules | 
|:--------| :-------- | 
|1.| [ec2-ansible](modules/ec2-ansible) | 
|2.| [ec2-goldengate](modules/ec2-goldengate) | 
|3.| [eks](modules/eks) | 
|4.| [mq](modules/mq) | 
|5.| [msk](modules/msk) |
|6.| [route53](modules/route53) |
|7.| [rds](modules/rds) |
|8.| [efs](modules/efs) |
|9.| [ecr](modules/ecr) |
|10.| [s3](modules/s3) |



- [ ] [Configure Volume Drivers](https://docs.gitlab.com/ee/user/project/repository/web_editor.html#create-a-file) 

## Installing Metrics Server 

- Please install metric server for the HPA to collect CPU and Memory metrics for pod autoscalling

```
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```
## Enabling Logging

- [ ] [Default Fargate Logging](https://docs.aws.amazon.com/eks/latest/userguide/fargate-logging.html)

## Addind AWS Loadbalancer Controller

- Please install loadbalancer controller to enable loadbalancers to work with EKS clusters

- [ ] [Setup Loadbalancer Controller in EKS Cluster](https://aws.amazon.com/premiumsupport/knowledge-center/eks-alb-ingress-controller-fargate/)

## Role Based Access

- Each groups in SSO gets a role created in respective aws accounts to which the group members can access

- These aws roles can be used to map with kubernetes user , the user with in cluster can either have Role/Cluster-Role mapped based on requirement

- Please refer the sample template created for **Non-Prod-Developer** group with only read access to a particular namespace *fargate-node* 

    - Sample Template: [role-based-access](Archive/role-based-access)
    - Reference Link: [Limited-access-to-IAM-user](https://www.freecodecamp.org/news/adding-limited-access-iam-user-to-eks-cluster/)


