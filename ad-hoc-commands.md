## Ad-Hoc Commands

Ad-hoc commands are one-off commands that you can run on one or more servers, from Ansible

They are useful for situations where you only need to do one or two actions, and don't need the complexity of a playbook.

### Structure:

ansible _group_ -m _module_ -a _arguments_

_By default ansible will run the Command module to run your commands

### Example:
```
ansible web-servers -m ping
```
This will run the ping module on all of the hosts in the web-servers group.

The result should look like the following:
```
node4.blinklab.ca | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
node3.blinklab.ca | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
node2.blinklab.ca | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

_Pay attention to the fact that the result shows "changed":false_
_This tells us that there was no change to the state of the server, only that a ping was performed._

A more complex ad-hoc command is this one for example:
```
sudo ansible web-servers -m yum -a "name=vim state=present" --become --ask-become-pass
```
What is happening here?
- '-m yum' says that we are using the yum module (yum package manager)
- '-a' lays out the arguments, those are package name=vim, and state=present
- --become and --ask-become-pass tells Ansible we need to sudo on the target servers, and to ask for the sudo password

The output of the command can be quite verbose.  That is, unless VIM is already installed, then Ansible will not install it again, this is what is called idempotence.








