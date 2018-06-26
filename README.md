# Documentation

This role used for deplaoy docker swarm stack.

+ [Quickstart](#Quickstart)
+ [Example requiremetns.yml file](#Ex1);
+ [Example host file](#Ex2);
+ [Examoke vars/main.yml](#Ex3);
+ [Playbook variables](#Table1);


## <a name="Quickstart"></a> Quickstart

[Install ansible](http://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) on the your host
Install python on the servers, if necessary  
You need to create a [requirements.yml](#Ex1) file and write down what roles are required in it. Then install roles from this file.
Install required rolles:  
```sh
$ ansible-galaxy install -r requirements.yml
```
Clone this repository in your directory:

```sh
$ git clone https://github.com/unicanova/ansible-docker-swarm
$ cd ansible-docker-swarm
```
Specify host addresses in the file /etc/ansible/hosts.  
Create a [site.yml](#Ex3) file, where you can specify the which template use for deplaoy docker swarm stack.  
In the playbook site.yml you can override varibales according to the [table](#Table1), if necessary.  

Execute command:  

```sh
$ ansible-playbook site.yml -b --extra-vars "ansible_sudo_pass=yourPassword"
```
#### <a name="Ex1"></a> Example requirements.yml:
```sh
- src: https://github.com/unicanova/ansible-docker-swarm
  version: master
  name: ansible-docker-swarm
```

#### <a name="Ex2"></a> Example hosts file:

```sh
[jenkinsmaster]
192.168.122.123 ansible_ssh_port=22 ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa

[jenkinslave]
192.168.122.77 ansible_ssh_port=22 ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa
```
#### <a name="Ex3"></a> Example site.yml:
```sh
- hosts: test
  roles:
    - ansible-docker-swarm
  vars_from: 
    - registry.yml
```

#### <a name="Table1"></a> Playbook variables
| Variable name | Variables description |
| ------------- | --------------------- |
| docker_registry_url | registry url |
| docker_registry_username | your docker registry user name |
| docker_registry_password | your password for login into registry |
| docker_registry_username_email | your email (not required) |
| docker_regisry_reauth | make reauth or not each time when role will be started |
| stack_directory |  | 
| swarm_user |  |
| swarm_group |  |
| docker_compose_template | file name for deploy swarm |
| stack_name | docker stack name | 
