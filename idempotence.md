## Idempotence

One of the strengths of Ansible is the idea of **idempotence**.  

The definition of idempotence is that an action can be applied multiple times without changing the result beyond the initial application.  

Let's use the example of VIM that we installed. If we attempt to install it again, Ansible will not just install it over again, it will check (gather facts) and discover that it is installed, and not change the state of the server.

So if we run this command again
```
sudo ansible web-servers -m yum -a "name=vim state=present" --become --ask-become-pass
```
The result of this command will be this:
```
node4.blinklab.ca | SUCCESS => {
    "changed": false,
    "msg": "",
    "rc": 0,
    "results": [
        "2:vim-enhanced-7.4.160-2.el7.x86_64 providing vim is already installed"
    ]
}
node2.blinklab.ca | SUCCESS => {
    "changed": false,
    "msg": "",
    "rc": 0,
    "results": [
        "2:vim-enhanced-7.4.160-2.el7.x86_64 providing vim is already installed"
    ]
}
node3.blinklab.ca | SUCCESS => {
    "changed": false,
    "msg": "",
    "rc": 0,
    "results": [
        "2:vim-enhanced-7.4.160-2.el7.x86_64 providing vim is already installed"
    ]
}
```
Note the **"changed":false** message.  -- this tells us nothing has changed, because VIM is already installed.