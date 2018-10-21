# vmware-guest

Deploys a new VM from a VMware template.

* Requires DHCP
* Optional second disk
* Checks for SSH port up at the end

## Getting Started

### Prerequisites

* Ansible

### Installing

```
$ ansible-galaxy install robrowan.vmware-guest
```

## Use

### Role Variables

Defaults

```
---
vmguest_state: poweredon
vmguest_disk_size: 20
vmguest_memory: 2048
vmguest_num_cpu: 1
vmguest_vlan: SERVERS
vmguest_template: centos7
vmguest_wait_for_ip_address: no
```

### Environment specific variables

Details of you vcenter/ESXi host:

```
vcenter_hostname: vcenter.domain
vcenter_datacenter: DATACENTER
vcenter_cluster: CLUSTER
vcenter_folder: /
vmguest_datastore: DATASTORE
```

Login creds, save in vault file:

```
vcenter_username: "ansible@vsphere.local"
vcenter_password: "password"
```

### Example playbook

```
- hosts: all
  roles:
    - robrowan.vmware_guest
```

## Authors

* **Rob Rowan** - [RobRowan](https://github.com/robrowan)

## License

This project is licensed under the MIT License.
