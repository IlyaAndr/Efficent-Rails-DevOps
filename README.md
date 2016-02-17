# Efficient Rails DevOps

Example app following the [Efficient Rails DevOps](http://www.efficientrailsdevops.com/) book by [Michael Trojanek](http://www.relativkreativ.at/about).

## Get up and running

- Clone the repo and change into the directory
- Run `vagrant up` to start the VM
- Start the playbook with `ansible-playbook -i inventories/staging site.yml --ask-vault-pass`
    - to run an individual tags, use  `ansible-playbook -i inventories/staging --tags TAG_NAMES_HERE site.yml --ask-vault-pass`
- Update the yum packages using `ssh root@192.168.1.100 "yum -y update"`
- `ssh root@192.168.1.100 "touch /.autorelabel && reboot"` will relabel our filesystem (which only needs to happen once)

## IMPORTANT

This repo uses [ansible-vault](http://docs.ansible.com/ansible/playbooks_vault.html) to encrypt its configuration and other sensitive information, but seeing as the password used to encrypt it is made public (listed below, and in the book), it is not advised you use it *as is*, and instead re-encrypt the relevant files yourself.

### Ansible Vault

- Password `erdo`

- To create a new vault, run `ansible-vault encrypt path/to/file`
- To edit a vault file, run `ansible-vault edit path/to/file`

#### Encrypted files

- `group_vars/all`

### Generate crypted password (for root_password task)

    python -c 'import crypt; print crypt.crypt("PASSWORD_HERE", crypt.mksalt(crypt.METHOD_SHA512))'

## IP address

This repo is based on the IP subgroup of `192.168.253.*`. If your subgroup is different and you need to modify the IP address, you'll need to update both the `Vagrantfile` and `inventories/staging` files.

## Installing Ansible

```bash
pip install --upgrade pip
php install ansible
```

### No Python?

If the commands above don't work, you probably don't have Python installed. The book recommends you use [pyenv](https://github.com/yyuu/pyenv) to install python, as it'll give you the ability to switch between different version, much like the benefits obtained by using rbenv.

For a a quick and dirty install process on OS X:

```bash
brew update
brew install pyenv
```

At this point it's important to note the set-up instructions provided by the installer.

```bash
pyend install 2.7.10
pyenv global 2.7.10
```
