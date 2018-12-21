 
# Requirements
------------
  - Python
  - Pip
  - Ansible
  - Boto3 
    - Ansible depends on the Python module Boto3 to communicate with AWS API. You can install Boto3 using pip: ```pip install boto boto3```

# Project Structure
------------
## Two Ansible roles are created to privision an EC2 instance and deploy the Sinatra app. 

## Ansible roles:

  - **ec2**
    - This role creates a security group for the EC2 instance and provisions a Ubuntu 14.04 EC2 instance on AWS.  
    - See roles/ec2/README for more information on this role. 
  - **sinatra-app**
    - This role installs Ruby, Bundler and the Gems necessary for the Sinatra application and then deploys the app on the EC2 instance created by the ec2 role.
    - See roles/sinatra-app/README for more information on this role.

## Playbooks:

  - **provision_ec2.yml** calls the ec2 role to provision an EC2 instance. 
  - **deploy_sinatra_app.yml** calls the sinatra-app role to deploy the Sinatra app. 
  - **main.yml** calls both provision_ec2.yml and deploy_sinatra_app.yml.

# How to use this project
------------
## Setup

### AWS
  - Login to the AWS console as REA user (see email for account id and credentials for REA user)
  - Create a SSH key pair for the sinatra-app role to SSH to the EC2 instance. EC2 role also needs a key pair to create the EC2 instance. 
    1. go to EC2 Dashboard -> Key Pairs -> Create Key Pair
    2. Give the key pair a name called **REA-key** 
    3. Download the private key **REA-key.pem** file and copy it into the root directory of this project. 
    4. Set permission of REA-key.pem to 400 ```chmod 400 REA-key.pem```

    Note: The steps above are needed as the ansible.cfg file in the root directory of this project uses REA-key.pem ```private_key_file = ./REA-key.pem```
    The ec2 role also has a variable called **keypair** in **roles/ec2/defaults/main.yml** which is set to **REA-key** by default. ```keypair: REA-key```

### Ansible-vault 
  The AWS access key and secret key for the REA user is encrypted in roles/ec2/vars/aws-keys.yml. You need to create a file called vaultpasswrd to store the vault password so the AWS keys can be consumed by the ec2 role. 

  1. Create a file called vaultpassword in the root directory of this project and put the vault password (see email for password) into the file. 

## Run
------------
From the root directory of this project
    ```ansible-playbook -i hosts main.yml --vault-password-file ./vaultpassword```
 
 
 






