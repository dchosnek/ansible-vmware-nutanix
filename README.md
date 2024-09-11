# Ansible VMware

This repository contains some simple Ansible playbooks for adding nodes to vCenter and properly configuring the vCenter cluster. It is assumed these are Nutanix nodes using standard vswitches.

## How to run

The variables for each cluster are contained in their own file, so you just need to run the following to set up the cluster whose variables are contained in the file `wasp.yml`.

```
ansible-playbook create-vmware-cluster.yml -e "@cluster_wasp.yml"
```

I have encrypted the username and password in the cluster variable files. You an replace those with plain text copies of your username and password. If you choose to also encrypt your variables, you'll need to add the `--ask-vault-pass` argument to the end of the above command.

## Files in this repo

`ansible.cfg` contains a few directives to eliminate warnings associated with not having an inventory file. These playbooks all execute as `localhost`, so no inventory is needed.

`create-vmware-cluster.yml` is the playbook that creates the Datacenter and Cluster and adds the Nutanix nodes to that cluster. It also properly configures DNS on each of those nodes and creates the VLANs specified in the variable file.

`delete-cluster.yml` is a simple playbook that just deletes the VMware cluster. It can be done manually just as easily.

`map-nfs-share.yml` maps an NFS share as a datastore to each node.

## Vault

The variable files are encrypted with Ansible vault. The `ansible.cfg` file indicates that the vault password file is located at `vault-pass.txt`.

The encyrpted strings in the cluster variable files in this repo were encrypted as shown below and as documented [here](https://docs.ansible.com/ansible/2.9/user_guide/vault.html#use-encrypt-string-to-create-encrypted-variables-to-embed-in-yaml)

```
ansible-vault encrypt_string --vault-password-file vault-pass.txt 'mypassword' --name 'vcenter_password'
```