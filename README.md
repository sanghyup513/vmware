# Ansible.fast-k3s

TBD   
   
> this playbook was tested on centos 7.7.   

# This doc is draft.
   
* install requirements   
```console
$ pip install -r requirements.txt
```
   
* change variable file
```console
$ vi vm_information.yml
---
### variable information 'vcenter'
vcenter_server: "vc.changeme.com"
vcenter_user: "Administrator@vsphere.local"
vcenter_pass: "password"
datacenter_name: "Datacenter"
cluster_name: "Cluster"
datastore_name: "Datastore-1"
vm_network: "VM Network"

### variable 'virtual machine"
vm_template: "c7.7-template"
vm_netmask: "255.255.255.0"
vm_gateway: "192.168.0.1"
vm_dns: "1.1.1.1"
```
   
* change inventory file   
```console
[nodes]
10.50.1.260	 vm_ipaddr=10.50.1.260
10.50.1.261	 vm_ipaddr=10.50.1.261
10.50.1.262	 vm_ipaddr=10.50.1.262

[nodes:vars]
ansible_ssh_user=root
ansible_ssh_pass=password
ansible_ssh_common_args="-o GlobalKnownHostsFile=/dev/null -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no"
```
   
# Warning
***if install k3s, system will rebooted.***   
   
* deploy lab environment 'k3s'
```bash
$ ansible-playbook -i inventory deploy-k3s.yml 
```
   
* (option) only deploy vm   
```bash
$ ansible-playbook -i inventory deploy-k3s.yml -t vm
```
   
* (option) only install k3s
```bash
$ ansible-playbook -i inventory deploy-k3s.yml -t k3s
```
   
# Known Issue
* `Ubuntu` 
Setting the network with vmware_guest in Ubuntu 18.04 (and latest) is known to be broken, due to missing support for `netplan` in the `open-vm-tools`.   
[https://docs.ansible.com/ansible/latest/scenario_guides/vmware_scenarios/vmware_troubleshooting.html](https://docs.ansible.com/ansible/latest/scenario_guides/vmware_scenarios/vmware_troubleshooting.html)    
   
# TO-DO
* select option `reboot`   
* update `readme.md`   
