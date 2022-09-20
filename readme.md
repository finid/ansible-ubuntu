# Automate Initial Server Setup of Multiple Ubuntu 22.04 Servers Using Ansible

This playbook shows how to automates the initial server setup of Ubuntu 22.04 servers using Ansible. It implements all the steps given in the [Initial Server Setup Guide for Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-20-04) tutorial, then adds a few more steps to make the server more secure.

Variables required to execute some parts of the playbook are specified in the `vars/default.yml` variable file. You'll need to modify the default Ansible inventory, or hosts, file (`/etc/ansible/hosts`) on your local machine so that it contains the IP addresses of the target hosts. 

## Settings

The following variables are defined in `vars/default.yml`.

- `create_user`: the name of the remote user to create.
- `ssh_port`: the custom port for logging into the hosts after the initial server setup.
- `copy_local_key`: path to a local SSH public key that will be copied as authorized key for the new user. By default, it copies the key from the home directory of the user running Ansible.


## Running this Playbook

Quick Steps:

### 1. Obtain the playbook

```shell
git clone
```

```shell
cd ansible-ubuntu
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
ansible-playbook --syntax-check initial.yml
```

Then run the the playbook.

```command
ansible-playbook --ask-vault-pass initial.yml
```

### 4. Run the other playbook

As a bonus, another playbook is included that you can use to maintain the servers after the initial server setup.

```command
ansible-playbook --syntax-check ongoing.yml
```

Then run the the playbook.

```command
ansible-playbook --ask-vault-pass ongoing.yml
```

For more information on how to run this Ansible setup, please check this guide: [Initial Server Setup Guide for Ubuntu 22.04](#).
