## Basic Playbook


Below is a basic playbook to install and enable HTTPD (apache web server), install and enable firewalld, and open ports 80 and 443 on firewall.

```
---
# Basic Apache httpd setup playbook
# install & enable httpd
# + install & enable firewalld
# + open firewall ports 80 and 443
# version 1.0
# scottrobarts
# April 2018

- hosts: web-servers
  become: yes

  tasks:
  - name: Install httpd
    yum: name=httpd state=present

  - name: http service state
    service: name=httpd state=started enabled=yes

  - name: Install firewalld
    yum: name=firewalld state=present

  - name: Enable firewalld
    service: name=firewalld state=started enabled=yes

  - name: insert firewalld rule for http
    firewalld: port=80/tcp permanent=true state=enabled immediate=yes

  - name: insert firewalld rule for https
    firewalld: port=443/tcp permanent=true state=enabled immediate=yes
```
So, what is happening here?

1. We are telling Ansible to run this playbook on our "web-servers" group in our hosts file
2. We are telling Ansible to sudo - "become: yes"
3. We are installing httpd
4. We are enabling the httpd service
5. We are installing firewalld
6. We are enabling the firewalld service
7. We are enabling port 80 of firewalld
8. We are enabling port 443 of firewalld

This playbook is run by issuing the following command:
```
ansible-playbook apache.yml --ask-become-pass
```
This command tells Ansible to run the playbook "apache.yml" and ask for the sudo password when it does so.

The playbook can be run again and again, and it won't do this actions again and again, because of idempotence.  If httpd is installed already, it won't install it again, it will gather facts (gathering the state of the server), and determine that httpd is installed already.

If you want to play around with this, you could issue an ad-hoc command to uninstall Apache httpd from node 2:
```
sudo ansible node2 -m yum -a "name=httpd state=absent" --become --ask-become-pass
```
Then re-run the playbook "apache.yml".  It will detect that Apache httpd is missing from node2 and reinstall it.


