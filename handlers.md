## Handlers

Handlers are basically tasks, and can do anything that tasks can do, but will only run when called from another task.

Example:
```
---
- hosts: local
    sudo: yes
    tasks:
    - name: Install Nginx
      apt: pkg=nginx state=installed update_cache=true
      notify:
        - Start Nginx

  handlers:
  - name: Start Nginx
    service: name=nginx state=started
```
In the above example "Start Nginx" will only be run when notified by "install Nginx"