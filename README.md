# Automating Cost-Efficiency: Stop Wasting Money on Idle EC2 Instances

#### This guides you through creating and managing AWS EC2 instances programmatically using Python. We'll cover launching instances, stopping them, and leveraging tags for automated control.

## install dependencies
```
pip install boto3

pip install awscli
```

## 1. Create EC2 instances
```
import boto3

ec2 = boto3.client('ec2')

image_id = 'ami-051f8a214df8bc123'  # Replace with your desired AMI ID
instance_type = 't2.micro'
key_name = 'my-key-pair'  # Replace with your key pair name

instances = ec2.create_instances(
    ImageId=image_id,
    InstanceType=instance_type,
    MinCount=2,
    MaxCount=2,
)

print(f"Instance IDs: {instances}")
```

## 2. Start Instances

```
ec2.Instance('i-241f8a213df8bc056').start()
ec2.Instance('i-441f8a213df8bc322').start()
```

## 3. Stop Instances
```
ec2.Instance('i-241f8a213df8bc056').stop()
ec2.Instance('i-441f8a213df8bc322').stop()
```

## 4. Start Instances based on tags
```
ec2_filter=[{'Name': 'tag:dev', 'Values': ['ec2_automation']}, {'Name': 'instance-state-name', 'Values': ['stopped']}]

ec2.instances.filter(Filters=ec2_filter).start()
```

## 5. Stop Instances based on tags
```
ec2_filter=[{'Name': 'tag:dev', 'Values': ['ec2_automation']}, {'Name': 'instance-state-name', 'Values': ['running']}]

ec2.instances.filter(Filters=ec2_filter).stop()
```
