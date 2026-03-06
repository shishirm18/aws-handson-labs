### To obtain the list of EC2 Instance names in the account

```bash
aws ec2 describe-instances --query 'Reservations[*].Instances[*].Tags[*].Value' --output text
```

### There is an EC2 instance name hey-ec2, change the instance from t2.micro to t2.nano

Step 1: Obtain the instance ID
```bash
INSTANCE_ID = $(aws ec2 describe-instances --filters 'Name=tag:Name,Values=hey-ec2' --query 'Reservations[*].Instances[*].InstanceId' --output text)
```

Step 2: Stop the EC2 Instance
```bash
aws ec2 stop-instances --instance-ids $INSTANCE_ID

#wait until it is fully stopped
aws ec2 wait instance-stopped --instance-ids $INSTANCE_ID
```

Step 3: Change the instance type to t2.nano
```bash
aws ec2 modify-instance-attribute --instance-id $INSTANCE_ID --instance-type "Value=t2.nano"
```

### There is an EC2 instance named hey-ec2 under us-east-1 region, enable the stop protection for this instance

Step 1: Check the status of EC2 instance
```bash
aws ec2 describe-instance-attribute --instance-id $(aws ec2 describe-instances --filters 'Name=tag:Name,Values=hey-ec2' --query 'Reservations[*].Instances[*].InstanceId' --output text) --attribute disableApiStop
```

Step2: Enable the stop protection for EC2 instance
```bash
aws ec2 modify-instance-attribute --instance-id $(aws ec2 describe-instances --filters 'Name=tag:Name,Values=hey-ec2' --query 'Reservations[*].Instances[*].InstanceId' --output text) --disable-api-stop
```