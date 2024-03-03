# Red Hat Ansible Automation Platform

Automation controller

AWX 

:arrow_right: Ansible Control Node

:arrow_right: Ansible Managed Nodes :Also referred to as ‘hosts’, these are the target devices (servers, network appliances or any computer) you aim to manage with Ansible.

Host: A remote machine managed by Ansible.

Group: Several hosts grouped together that share a common attribute.

Inventory: A collection of all the hosts and groups that Ansible manages. Could be a static file in the simple cases or we can pull the inventory from remote sources, such as cloud providers.

Modules: Units of code that Ansible sends to the remote nodes for execution.

Tasks: Units of action that combine a module and its arguments along with some other parameters.

​​Playbooks: An ordered list of tasks along with its necessary parameters that define a recipe to configure a system.

Roles: Redistributable units of organization that allow users to share automation code easier.

YAML: A popular and simple data format that is very clean and understandable by humans.

---
Ansible Inventory
> /etc/ansible/hosts

  [hosts](https://github.com/krimsoda/ansible/blob/01f0ab4fa43050f95956f19b277883bedd7e1d69/hosts)
  
> /etc/ansible/ansible.cfg

[ansible.cfg](https://github.com/krimsoda/ansible/blob/6e0c1ab6d46af67e8a75be20ba6e6f8debe4e6f3/ansible.cfg)
`etst`

---

Preparing:


(Ansible Control Node)

#passwordless SSH authentication
* Generate a key pair
```
ssh-keygen
```
* Add public key to Managed Node
```
ssh-copy-id ansible@managed node ip address
```


(Ansible Managed Nodes)
```
useradd ansible
```
```
passwd ansible
```
```
echo 'ansible ALL=(ALL) NOPASSWD:ALL'>/etc/sudoers.d/ansible
```
----
Ad-Hoc Commands

Create User (redhat)
```
ansible -i inventory ansible1 -m user -a "name=ansible" -u root -k
ansible -i inventory ansible1 -m shell -a "echo 'ansible:password' | passwd --stdin ansible" -u root -k
```
Create User (ubuntu)
```
ansible -i inventory ubuntu -m user -a "name=ansible" create_home=yes -u student -b -k -K
ansible -i inventory ubuntu -m shell -a "echo 'ansible:password'| chpasswd" -u student -b -k -K
```
Verify User (ansible)
```
ansible -i inventory all -m command -a "id" -u ansible
ansible rocky -m command -a "ls -l /root"
```
---
Ansible adhoc Command Structure

`ansible [target_hosts] -m [module] -a "[arguments]" [flags]`

`ansible server -m file -a "dest=/root/.ssh/authorized_keys state=absent"`




