# vmware-guest

Deploys a new VM from a VMware template.

* DHCP or static IP addresses
* Configurable number of disks and datastores
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
vmguest_disks:
    - size_gb: "{{ vmguest_disk_size }}"
      type: thin
      datastore: "{{ vmguest_datastore }}"
vmguest_networks:
    - name: "{{ vmguest_vlan }}"
      type: dhcp
      domain: ".lan"
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

### Static IP address

The default is to use DHCP. To set a static IP address per host, use a host_var such as:

vmguest_networks:
    - name: "VM Network"
      ip: "192.168.1.10"
      netmask: "255.255.255.0"
      gateway: "192.168.1.1"
      dns_servers:
       - "192.168.1.1"

### Multiple disks

Default is a single 20GB disk. Example of multiple disks:

vmguest_disks:
    - size_gb: 20
      type: thin
      datastore: "{{ vmguest_datastore }}"
    - size_gb: 100
      type: thin
      datastore: "{{ vmguest_datastore }}"
    - size_gb: 2000
      type: thin
      datastore: nas01

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
