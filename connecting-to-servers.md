## Configuring connections to target servers

### Creating the Ansible user

We want to create a non-root user on the target machines that Ansible will use for running commands

When Ansible is running commands it will default to trying to connect to the target servers over SSH using the user it is running as

You can create a playbook to do this, and there is one in the sample files on Github. But below are the commands to do this on one of the hosts.

Login to the servers. I have disallowed root SSH so I login as srobarts, a user I created with sudo privileges
Once logged in run these commands:
```
useradd ansible 
passwd ansible 
usermod -a -G wheel ansible
```
The sudoers configuration will need to setup to allow users of the group wheel to run all commands.

### Key-based authentication to servers

Then from the Ansible controller server (where Ansible is installed), we will need to share the public key established on that server with the two target servers.
```
ssh-copy-id ansible@192.168.0.1
```
