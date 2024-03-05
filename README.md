# Red Hat Ansible Automation Platform

Automation controller

AWX 

Ansible Galaxy

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
Ansible Config File

> /etc/ansible/ansible.cfg

[ansible.cfg](https://github.com/krimsoda/ansible/blob/6e0c1ab6d46af67e8a75be20ba6e6f8debe4e6f3/ansible.cfg)

> /etc/ansible/hosts

[hosts](https://github.com/krimsoda/ansible/blob/01f0ab4fa43050f95956f19b277883bedd7e1d69/hosts)
  

`etst`

---

Preparing:


(Ansible Control Node) Ansible account

#passwordless SSH authentication
* Generate a key pair specifically used for Ansible
```
ssh-keygen -t ed25519 -C "ansible"
```
* Add public key to Managed Node
```
ssh-copy-id -i ~/.ssh/ansible.pub ansible@<IP Address>
```
---

(Ansible Managed Nodes) Ansible account manual create
```
useradd ansible
```
```
passwd ansible
```
```
echo 'ansible ALL=(ALL) NOPASSWD:ALL'>/etc/sudoers.d/ansible
```
```
sudo -l -U ansible
```
----
Ad-Hoc Commands

Create User (redhat)
```
ansible -i inventory ansible1 -m user -a "name=ansible" -u root -k
ansible -i inventory ansible1 -m shell -a "echo 'ansible:password' | passwd --stdin ansible" -u root -k
```
Create User (debian)
```
ansible -i inventory debian -m user -a "name=ansible create_home=yes" -u student -b -k -K
ansible -i inventory debian -m shell -a "echo 'ansible:password'| chpasswd" -u student -b -k -K
```
Verify User (ansible)
```
ansible -i inventory all -m command -a "id" -u ansible
ansible rocky -m command -a "ls -l /root" -b
```
Privilege escalation
```
ansible rocky -i inventory -u root -k -m copy -a "src=/etc/sudoers.d/ansible dest=/etc/sudoers.d/ansible
ansible debian -i inventory -u root -k -b -K -m copy -a "src=/etc/sudoers.d/ansible dest=/etc/sudoers.d/ansible
```
---
Ansible adhoc Command Structure

`ansible [target_hosts] -m [module] -a "[arguments]" [flags]`

`ansible server -m file -a "dest=/root/.ssh/authorized_keys state=absent"`

-m: module -a: option accepts options either through the key=value syntax or a JSON string starting with { and ending with } for more complex option structure.  -C: check 

Query package version

`ansible all -m command -a'/usr/bin/rpm -qi <PACKAGE NAME>' | grep 'SUCCESS\|Version'`

---
Ansible Playbook
```
ansible-playbook -i inventory adduser.yaml -u root -k -vv
```
-b :become sudo -K :sudo password -k :User/ssh password #root username not required -b -K refer ansible.cfg



