## Installing Ansible

### On CentOS/Redhat Linux

```
sudo yum -y install epel-release
sudo yum -y install ansible
```

### On Ubuntu/Debian
```
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible
```

### On Mac
( Using Homebrew: https://brew.sh/ )
```
brew install ansible

```
Then add an 'ansible.cfg' file to the location ~/.ansible
With the following contents:

```
[defaults]
stdout_callback = yaml
connection = smart
timeout = 60
deprecation_warnings = False
host_key_checking = False
retry_files_enabled = False
inventory = /Users/scottrobarts/code/ansible/hosts
```
Assuming you are going to keep your inventory file in ~/code/ansible/hosts




