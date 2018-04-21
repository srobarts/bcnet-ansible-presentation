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

To check to see all users of the group 'wheel' run this command:
```
sudo grep 'wheel' /etc/group
```

### Key-based authentication to servers

Once we have created the ansible user, we can move on to creating and sharing our SSH keypair

First we need to create our keypair:
```
sudo ssh-keygen -t rsa
```
The process will prompt you for some information. You can accept most of the defaults.

You can choose whether or not you want to use a keyphrase, a keyphrase adds more security, but is not required.

Your public key is now here:
```
/home/ansible/.ssh/id_rsa.pub
```
And your private key is here:
```
/home/ansible/.ssh/id_rsa
```
**_Never, ever, ever, share your private key_**

Next we will need to share the public key with our target servers.  This can be done with the following command:
```
ssh-copy-id ansible@159.89.126.191
```
_This assumes the ansible user is already created on the target server, and we can SSH as this user._

If you are a Mac user, you will need to install ssh-copy-id using Homebrew:
```
brew install ssh-copy-id
```
You can also copy over the public key using this command:
```
cat ~/.ssh/id_rsa.pub | ssh demo@198.51.100.0 "mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >>  ~/.ssh/authorized_keys"
```
### Setting up your Ansible user

There is another step before we are ready to communicate with our server via Ansible

By default Ansible will try to communicate with the servers via which ever user it is running as.  I usually sudo to root when I am doing administration, but on the servers I want Ansible to run as the ansible user. We solve this problem by creating a variable.

- In your /etc/ansible directory create a directory called 'group-vars'
- Then in that directory create a file called 'all'
- Add the following lines to the 'all' file
```
---
ansible_ssh_user: ansible
```
This is a YAML formatted file, so the three dashes at the top are necessary, don't forget them. The directive in this file 'ansible_ssh_user' tells Ansible to use the user ansible on the servers it is altering

Ansible should now be able to communicate with the target servers, from the controller server.

We will test this in the next section with the Ansible Ping module.

