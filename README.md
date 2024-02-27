# IaC Project Terraform Ansible: Integrate Ansible Playbook Execution in Terraform


We use Terraform to automatically create an EC2 instance and we switch back to our Ansible project to execute our Ansible playbook there: 

<img width="522" alt="Screenshot 2024-02-28 at 00 05 41" src="https://github.com/redjules/IaaC-Project-Terraform-Ansible/assets/106017493/4c315905-82a2-4618-894e-ca77b99cabf1">

Manual tasks between provisioning and configuring:

1) We get the IP address manually from TF output

2) Update the hosts file manually

3) Execute Ansible command


But we will automate them with Terraform and Ansible

