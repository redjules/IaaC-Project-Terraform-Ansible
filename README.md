# IaC Project Terraform Ansible: Integrate Ansible Playbook Execution in Terraform


We use Terraform to automatically create an EC2 instance and we switch back to our Ansible project to execute our Ansible playbook there: 

<img width="522" alt="Screenshot 2024-02-28 at 00 05 41" src="https://github.com/redjules/IaaC-Project-Terraform-Ansible/assets/106017493/4c315905-82a2-4618-894e-ca77b99cabf1">

Manual tasks between provisioning and configuring:

1) We get the IP address manually from TF output

2) Update the hosts file manually

3) Execute Ansible command


But we will automate them with Terraform and Ansible

we will use a local_exec provisioner:


![Screenshot 2024-02-28 at 18 15 57](https://github.com/redjules/IaaC-Project-Terraform-Ansible/assets/106017493/60cbdb66-73cf-4523-942c-cb6fd8b5ba9b)


![Screenshot 2024-02-28 at 18 16 23](https://github.com/redjules/IaaC-Project-Terraform-Ansible/assets/106017493/75352763-182a-4ed4-a679-7621bb124d4e)

we overwrite the host file with the command inventory:

![Screenshot 2024-02-29 at 09 59 49](https://github.com/redjules/IaaC-Project-Terraform-Ansible/assets/106017493/2fae4010-5cd5-4e22-9809-6e057dbfc754)


![Screenshot 2024-02-29 at 10 00 22](https://github.com/redjules/IaaC-Project-Terraform-Ansible/assets/106017493/13c13a03-5b84-49fc-bed8-28d70dfaaff4)

we change to all the hosts:

![Screenshot 2024-02-29 at 10 03 49](https://github.com/redjules/IaaC-Project-Terraform-Ansible/assets/106017493/aa1bfe68-65b2-4d46-87ec-fa870d5d8c87)


we have ll the containers running from the server:

![Screenshot 2024-02-29 at 10 02 24](https://github.com/redjules/IaaC-Project-Terraform-Ansible/assets/106017493/f7e8d78b-f3d8-4c06-9550-e0a2ce7030f4)

Using provisioners are not the recommended way in Terraform because terraform has no control over the provisioners so it cannot manage the state. One of the problems we have with provisioners is the timing issue. By the time the resource is executed, the EC2 instance may not be fully created and initialized. 


![Screenshot 2024-02-29 at 10 09 45](https://github.com/redjules/IaaC-Project-Terraform-Ansible/assets/106017493/3774792a-0580-44a7-b467-d04d08a14afd)


![Screenshot 2024-02-29 at 10 10 05](https://github.com/redjules/IaaC-Project-Terraform-Ansible/assets/106017493/59afa50a-da2f-45c2-843e-b27e6a93380c)

we create a new task to solve that with "wait for", that let's us configure a crtierium or a kind of logic that tells Ansible to wait for this logic to be true before executing the next play or task.

![Screenshot 2024-02-29 at 10 15 21](https://github.com/redjules/IaaC-Project-Terraform-Ansible/assets/106017493/0d2e6118-da39-448a-a391-ce5ce035da4f)

we execute:


![Screenshot 2024-02-29 at 10 16 35](https://github.com/redjules/IaaC-Project-Terraform-Ansible/assets/106017493/676d536a-1560-403b-bc9f-7fe962331852)

another wy to use a provisioner is by using null_resource:

![Screenshot 2024-02-29 at 10 19 26](https://github.com/redjules/IaaC-Project-Terraform-Ansible/assets/106017493/34c99265-843f-404a-8641-1438c63b3070)


we could install a trigger too to tell Terraform when to run that resource:


![Screenshot 2024-02-29 at 10 21 33](https://github.com/redjules/IaaC-Project-Terraform-Ansible/assets/106017493/7c0a8d62-5134-4bb8-b4b4-91d6e3ea21c4)

we do terraform init and terraform apply:

![Screenshot 2024-02-29 at 10 22 29](https://github.com/redjules/IaaC-Project-Terraform-Ansible/assets/106017493/8aeac2dd-6102-4b57-a52a-35994e3d2bbf)

the resource was executed as last component

![Screenshot 2024-02-29 at 10 23 05](https://github.com/redjules/IaaC-Project-Terraform-Ansible/assets/106017493/39be47dd-5971-406d-9144-db6d4f329f0a)

if now we ssh into the server, we should see all the containers running again:

![Screenshot 2024-02-29 at 10 25 21](https://github.com/redjules/IaaC-Project-Terraform-Ansible/assets/106017493/234e144e-7073-436d-95e6-6a8d0a955973)


