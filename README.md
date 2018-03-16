# ansible_sample
Ansible playbook to create aws ec2 instance and install nginx

# Assumptions
1. Using Amazon AMI image
2. Ansible version 2.2.1
3. Outbound port 80 open in ACL ,
4. we need private key  stored in AWS account and give local path in common.yml
5. AWS credentials stored in ~/.aws/credentials in following format
```
[default]
aws_access_key_id = AKIXXXXXXXXXXXXX
aws_secret_access_key = FHhCXXXXXXXXXXXXXXXXXXXXXX
```


#Part 1: Creating EC2 instance
```
export ANSIBLE_HOST_KEY_CHECKING=False && ansible-playbook -i hosts apps/sample1/playbooks/create.yml

```

This command

1. Create Security Group on AWS and open port 80, 443 and 22
2. Creates Ec2 instance on AWS and add that security Group
3. After Ec2 is created , it install some basic yum packages , install nginx , copy sample nginx conf ,site1.conf, index.html to instance
4. Webpage can be seen at http://ipaddress  of instance



#Part2: Updating Existing instance
```
export ANSIBLE_HOST_KEY_CHECKING=False && ansible-playbook -i hosts apps/sample1/playbooks/update.yml

```

1. This command updates any existing machine centos or RHEL or Amazon AMI
2. We need to give , private key path and IP address of machine in hosts file

hosts file
```
[host_with_key]
13.211.141.52 ansible_ssh_user=ec2-user ansible_ssh_private_key_file=/Users/randhir/sshkeys/randhir-test.pem

```
