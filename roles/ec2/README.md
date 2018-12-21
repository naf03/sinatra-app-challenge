Ansible Role: EC2
=========

Provisions a Ubuntu 14.04 EC2 instance on AWS with a security group.

Requirements
------------
- Boto3 
 Ansible depends on the Python Module Boto3 to communicate with AWS API.
 You can install Boto3 using pip: 
 ```pip install boto boto3```

Role Variables
--------------
Variables that you can override are in defaults/main.yml and are explained below:
    
    keypair: REA-key
The name of the SSH key pair you created in AWS console
    
    security_group: sinatra_app_server_sg
The name of the security group attached to the EC2 instance
    
    region: ap-southeast-2
The region where the EC2 instance will be created in
    
    count: 1
The number of EC2 instances to create
    
    ssh_port: 22
The SSH port number for the EC2 instance
    
    http_port: 80
The http port number for the EC2 instance
    
    ssh_cidr_ip: 0.0.0.0/0
The IP range allowed to SSH to the EC2 instance
    
    http_cidr_ip: 0.0.0.0/0
The IP range allowed to access the Sinatra app running on port 80 via HTTP

Dependencies
------------

None

Example Playbook
----------------

    - hosts: local
      connection: local
      roles:
         - ec2

License
-------

BSD

Author Information
------------------

Alex Fan
