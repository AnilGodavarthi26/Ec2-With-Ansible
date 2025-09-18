# Ec2-With-Ansible
Created a ec2 instance with ansible and secured the password using ansible vault

Steps to Create an EC2 Instance using Ansible

Install boto3 > sudo apt install python3-boto3

Install the Ansible AWS collection > ansible-galaxy collection install amazon.aws --force

Create a role > ansible-galaxy role init <role_name>

Write the tasks required to create an EC2 instance inside the tasks folder of the role created above.

Store AWS credentials securely using Ansible Vault > ansible-vault create group_vars/all/pass.yml

This will prompt you to create and confirm a new vault password.

(Alternative way – not recommended)

Create a random password file for vault:

openssl rand -base64 2048 > vault.pass

Add AWS credentials using:

ansible-vault create group_vars/all/pass.yml --vault-password-file vault.pass

Note: Using this method may cause errors if the vault file is treated as an executable script or if line endings are set to CRLF instead of LF. To avoid this issue, stick with the first method.

Inside the vault file, store AWS credentials like this:

aws_access_key: YOUR_AWS_ACCESS_KEY
aws_secret_key: YOUR_AWS_SECRET_KEY

Reference variables in your playbook using {{ variable_name }}.
Example: instance_type: "{{ instance_type }}"

Run the playbook with Ansible Vault password prompt

ansible-playbook playbook.yml --ask-vault-pass

Provide the password.This will create an EC2 instance in AWS using Ansible.
