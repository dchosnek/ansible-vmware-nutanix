# Ansible VMware

This repository contains some simple Ansible playbooks for adding nodes to vCenter and properly configuring the vCenter cluster.

## How to run

The variables for each cluster are contained in their own file, so you just need to run the following to set up the cluster whose variables are contained in the file `wasp.yml`.

```
ansible-playbook create-vmware-cluster.yml -e "@wasp.yml"
```

## Files in this repo

`ansible.cfg` contains a few directives to eliminate warnings associated with not having an inventory file. These playbooks all execute as `localhost`, so no inventory is needed.

`create-vmware-cluster.yml` is the playbook that creates the Datacenter and Cluster and adds the Nutanix nodes to that cluster. It also properly configures NTP on each of those nodes.

`delete-cluster.yml` is a simple playbook that just deletes the VMware cluster. It can be done manually just as easily.

`map-nfs-share.yml` maps an NFS share as a datastore to each node.
