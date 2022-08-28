# Automate Initial Server Setup of Multiple Ubuntu 20.04 Servers Using Ansible

This playbook automates the initial server setup of Ubuntu 20.04 servers as explained in the manual version - 
[Initial Server Setup Guide for Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-20-04).

Variables required to execute some parts of the playbook are specified in the `vars/default.yml` variable file. You'll need to modify the default Ansible inventory, or hosts, file (`/etc/ansible/hosts`) on your local machine so that it contains the hostnames and or IP addresses of the target hosts. 

## Settings

The following variables are defined in `vars/default.yml`.

- `create_user`: the name of the remote user to create.
- `copy_local_key`: path to a local SSH public key that will be copied as authorized key for the new user. By default, it copies the key from the home directory of the user running Ansible.


## Running this Playbook

Quick Steps:

### 1. Obtain the playbook

```shell
git clone
```

```shell
cd ansible-playbooks/setup_ubuntu2004
```

### 2. Customize Options

```shell
nano vars/default.yml
```

```yml
#vars/default.yml
create_user: sammy
copy_local_key: "{{ lookup('file', lookup('env','HOME') + '/.ssh/id_rsa.pub') }}"
```

### 3. Run the Playbook

Best to perform a syntax-check of the playbook.

```command
ansible-playbook --syntax-check playbook.yml
```

Then run the the playbook.

```command
ansible-playbook -u root playbook.yml
```

For more information on how to run this Ansible setup, please check this guide: [Initial Server Setup Guide for Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-automate-initial-server-setup-on-ubuntu-20-04).
