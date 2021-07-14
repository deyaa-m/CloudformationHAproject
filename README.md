## Udagram Project

You can find udagram project here: [**s3://udacity-demo-1/udacity.zip**](s3://udacity-demo-1/udacity.zip)

### Project Diagram
![alt text](https://github.com/deyaa-m/CloudformationHAproject/blob/master/udacity-iac.jpg)
### Project Architecture
The project is split in two main parts:
1. udagram-infra.yaml: which holds the project infrastructure layer such as (VPC, Subnets, Gateways and Routes)
2. udagram-app.yaml: which holds the project application layer such as (instance launch condfigurations, Autoscaling)

### How to Provision Stacks:
1. ```aws cloudformation create-stack udagram-infra udagram-infra.yaml```  
2. ```aws cloudformation create-stack udagram-app udagram-app.yaml --capabilities CAPABILITY_NAMED_IAM```

### How to Delete Stacks:
1. ```aws cloudformation delete-stack udagram-app```
2. ```aws cloudformation delete-stack udagram-infra```

*ps*: wait untill first stack is provisioned/deleted before further action.

*update:* if you hate wating, I would suggest using this:

### Nested Stacks:

**Provision:**  ``` aws cloudformation create-stack --stack-name udagram-nest --template-body file://udagram-nest.yaml  --capabilities CAPABILITY_NAMED_IAM CAPABILITY_AUTO_EXPAND```

**Delete:** ```aws cloudformation delete-stack udagram-nest```
