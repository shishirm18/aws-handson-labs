### To obtain the list of EC2 Instance names in the account

```bash
aws ec2 describe-instances --query 'Reservations[*].Instances[*].Tags[*].Value' --output text
```

### There is an EC2 instance named hey-ec2 under us-east-1 region, enable the stop protection for this instance

Step 1: Check the status of EC2 instance
```bash
aws ec2 describe-instance-attribute --instance-id $(aws ec2 describe-instances --filters 'Name=tag:Name,Values=xfusion-ec2' --query 'Reservations[*].Instances[*].InstanceId' --output text) --attribute disableApiStop
```

Step2: Enable the stop protection for EC2 instance
```bash
aws ec2 modify-instance-attribute --instance-id $(aws ec2 describe-instances --filters 'Name=tag:Name,Values=xfusion-ec2' --query 'Reservations[*].Instances[*].InstanceId' --output text) --disable-api-stop
```