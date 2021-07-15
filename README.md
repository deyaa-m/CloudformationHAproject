## Udagram Project

Download udagram project: **[s3://udacity-demo-1/udacity.zip](s3://udacity-demo-1/udacity.zip)**

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

## update: Nesting

### Nested Stacks:

Following **Best Practices**, nesting was more reliable and automation oriented.

Running the following script will create a root stack with Infra and App stacks as chlidren.

**Provision:**  
``` 
aws cloudformation create-stack --stack-name udagram-nest \
--template-url https://udagram-nest.s3.eu-west-2.amazonaws.com/udagram-nest.yaml \
--parameters ParameterKey=MyIp,ParameterValue=$(curl -s http://checkip.amazonaws.com/)/32 \
--capabilities CAPABILITY_NAMED_IAM CAPABILITY_AUTO_EXPAND
```

Explainations: 

``` CAPABILITY_NAMED_IAM``` gives stack the capability of creating IAM Roles

```CAPABILITY_AUTO_EXPAND``` gives stack the capability of nesting

```Parameter``` it run a shell command to identify your local public IP address to use it as sourceip in Bastion SG

**Delete:** 

```aws cloudformation delete-stack udagram-nest```

## Udagram Link [http://udagram-ALB-MN8O2PYBRWVO-1164051927.eu-west-2.elb.amazonaws.com](http://udagram-ALB-MN8O2PYBRWVO-1164051927.eu-west-2.elb.amazonaws.com)
