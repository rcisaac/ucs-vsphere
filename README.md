# ucs-vsphere

A collection of roles built as an example playbook to implement some base vCenter and host configurations for a Cisco UCS Converged Infrastructure placement.

Example invocation:

`   ansible-playbook -i inventory site.yml    `

Role - vCenter
=========

Setup of a freshly deployed vCenter appliance, creating a datacenter, cluster, vDS, and some example vDS portgroups.

Role - HostAdd
=========

Add hosts to vCenter and the created vDS.  Broken off from HostConfig to be run in serial between hosts to prevent issues within vCenter.

Role - HostConfig
=========

Configured services, networking, and storage.

Requirements
------------

The VMware pyvmomi is required as well as the vSphere automation python sdk:

`    pip install pyvmomi`

`    pip install --upgrade git+https://github.com/vmware/vsphere-automation-sdk-python.git `

Expectation of invoking this playbook/roles is for a freshly provisioned vCenter instance (tested on vCenter 6.7 U2), as well as newly installed ESXi instances that have been configured with basic IP and VLAN information for the management interface of the ESXi host.

Role Variables
--------------

Variables need to be scrutinized to adjust to values appropriate to the intended environment.  At a minimum, the esxi_password and vcenter_password as well as appropriate username variables will need to be adjusted to what is set for the ESXi hosts and the vCenter. 

The example inventory file has host groups of 'esxi_fc' and 'esxi_iscsi' that are to be referenced as the hosts in the site.yml.  These example host groups include the appropriate vmkernel values to be set for the hosts, with iSCSI appropriate values being used if the 'configure_iscsi' variable is defined.  Additional iSCSI appropriate variables are specified in the variable file that will be referenced if 'configure_iscsi' is defined.  VMFS datastores can be added with the enablement of the 'configure_vmfs' variable.

Dependencies
------------

The roles listed have dependencies to run in the order specified in the site.yml

1. vCenter
2. HostAdd
3. HostConfig

License
-------

BSD

Author Information
------------------
Ramesh Isaac, Technical Marketing Engineer with UCS Data Center Solutions at Cisco
