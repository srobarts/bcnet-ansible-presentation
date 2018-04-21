# Setting up the hosts file

Ansible uses an inventory file called hosts to keep track of what servers it need to communicate with

You can use the default file, but I prefer to setup a simplified file.

Backup the sample hosts file:
```
sudo mv /etc/ansible/hosts /etc/ansible/hosts.orig
```
Create a new hosts file and open it for editing:
```
vim /etc/ansible/hosts
```
Add the web servers:
```
[web-servers]
159.89.126.191
159.89.123.40
```
The servers list consists of the group name - "web-servers" and the list of servers you wish to have in that group.

Using this functionality you can deal with groups of servers at once, by referring to the group name.

As an example, you can now test the connection to these servers with a ping command:
```
ansible all -m ping
```
The result should look like this: