# Introduction

This healthcheck uses Ansible playbooks and orachk framework as engine. It can be used on IaaS, DBCS or JCS instances running on top of Oracle Cloud Machine, Oracle Public Cloud (gen1) or Oracle Bare Metal Cloud.

# Use Case

The use case here is cloud infrastructure automation to perform a health check against IaaS, JCS and DBCS VMs/computes running Oracle Databases. Ansible Playbooks uses orachk as healthcheck framework to perform the checks - it generates json files that are parsed by playbooks, printing the findings that got WARNING or FAIL status. The Ansible Control Host can be a bastion VM running in the cloud.

# Pre-requisites 

* OL 6 or later
* Ansible 

# Installation

- Download & Install EPEL package from http://fedoraproject.org/wiki/EPEL

- Install Ansible on Control Host

```
rpm -e paramiko-1.13.0-1.noarch
yum install python-jmespath
yum install ansible
```

- Edit the inventory file on `/etc/ansible/hosts` and add the hosts grouped by type

```
[dbcs]
dbcs-vm1.example.com
dbcs-vm2.example.com

[iaas]
iaas-vm1.example.com
iaas-vm2.example.com

[jcs]
jcs-vm1.example.com
jcs-vm2.example.com
```

- Edit the configuration file `/etc/ansible/ansible.cfg` and uncomment out the line `stdout_callback = skippy`

- Create a folder on your Ansible Control Host

- Download the oracloud healthcheck and unzip the files inside of the folder created on the last step

- Download the latest version of `oracheck.zip` from MOS and upload to the same folder

# Running the healthcheck

- Navigate to the folder containing the oracloud healthcheck files
- Run the healthcheck

-> Perform HC on Cloud IaaS Linux hosts
`ansible-playbook iaas_playbook.yml`

-> Perform HC on Oracle Database Cloud Service hosts
`ansible-playbook dbcs_playbook.yml`

-> Perform HC on Java Cloud Service hosts
`ansible-playbook jcs_playbook.yml`

-> Perform HC on all (IaaS, DBCS, JCS) hosts
`ansible-playbook all_playbook.yml`

# Additional commands

-> Perform ad-hoc HC on particular hosts
`ansible-playbook iaas_playbook.yml --limit "<host1>,<host2>"`

