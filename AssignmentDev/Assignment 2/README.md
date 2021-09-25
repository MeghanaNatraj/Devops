# Ansible Playbook
### References: https://www.middlewareinventory.com/blog/ansible-git-example/
## STEP 1
#### Installing Ansible following the instructions in:
#### Installation guide: https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html
## STEP 2
#### Generating a personal access token in github referring to the below link:
#### [Create a personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
## STEP 3
#### Create a simple nodejs app and upload it in the private repository.
#### Referring to: [link](https://expressjs.com/en/starter/hello-world.html)
## STEP 4
#### Store the github username and token in a file using `ansible-vault`
#### 1. create a vault password and confirm it in  `$ ansible-vault create secrets.yml `
#### 2. Then a secrets.yml file will open. 
#### 3. Insert your gitusername and password in the same.
## STEP 5
#### Create an EC2 Instance on AWS.
#### Referring to: [Link](https://docs.aws.amazon.com/efs/latest/ug/gs-step-one-create-ec2-resources.html)
#### Remember while creating the instance, add a custom TCP rule with the port number you have given in your node app. You can also edit the rules afterwards if you haven't added it while creating the instance. Use the ssh client to connect to the instance.
## STEP 6
#### In your project directory create an inventory called ansible_hosts.
#### ` $ cd project_folder`
#### ` $ touch ansible_hosts`
#### Now open the ansible_hosts in a text editor and add the following code in the file:
#### Change the default user to EC2 user.
##### 1. [nodeserver]
##### PUBLIC IP ADDRESS HERE ansible_user=ubuntu ansible_port=22 ansible_ssh_private_key_file=
##### 2. [nodeserver:vars]
##### ansible_ssh_common_args="-o StrictHostKeyChecking=no"
## STEP 7
#### Create an ansible playbook 'gitexample.yml'. Change the following variables in the playbook:
#### 1. In the "Change the ownership of the directory part" change the owner to the name of your ec2 instance. For me it was 'ec2-user'.
#### [Set of default names](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connection-prereqs.html)
#### 2. In "validating the port is open" task change the port number to the port number you used in your node app. In "Download the NodeJs..." task change the path name to the path of your own private repository.
## STEP 8
#### Check if the hostgroup is reachable or not:
#### `$ ansible nodeserver -m ping -i ansible_hosts`
#### Now run the playbook using the following command:
#### `$ ansible-playbook gitexample.yml --ask-vault-pass`
## STEP 9
#### After the playbook runs successfully, open your app in the browser by typing this:
#### `http://<Public ip address>:<portnumber>`
