# Using Ansible to provision web servers and Wordpress sites
#### A BCNet Conference 2018 Presentation

Traditionally web servers were built by issuing specific commands via the command line, this was time consuming and could lead to errors and misconfiguration of servers. With the advent of configuration management tools this process has been automated. In this session I will show users how to provision a Linux web server and install Wordpress on that server using Ansible and WP-CLI in mere minutes. Ansible and WP-CLI and well-supported and free technologies available to all. I will also show users how to setup both systems on their own machines.

The fundamental issue is automation and consistency of configuration. Also there is the ability to spin up new machines in minutes.

Running the basic playbook:
```
ansible-playbook apache.yml --ask-become-pass
```

Running the wordpress playbook against node 3:

Note: node3 specification is in site.yml
```
ansible-playbook wordpress.yml --ask-become-pass
```


