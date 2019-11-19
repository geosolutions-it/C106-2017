# C106-2017

Ansible Automation

## Requirements

**Manager node:**

- Ubuntu 18.04
- Python Python 2.7.15+
- SSH
- Ansible 2.9

**Managed nodes:**

- Ubuntu 18.04
- SSH

## Environment setup

Ansible by default manages machines over SSH and assumes SSH keys are being used.
Ansible only needs to be installed on a machine to be able to manage other machines and it doesn't leave software installed or running on managed machines.

### Install Python
```sh
sudo apt update
sudo apt install python
```

### Install Ansible via pip

Install Pip

```sh
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python get-pip.py --user
echo "PATH=$PATH:/home/ubuntu/.local/bin/pip" >> ~/.bashrc
```

Then install ansible

```sh
pip install --user ansible
ansible --version
```

## Credentials

The purpose of the credentials folder is to store sensitive data. The file 'id_rsa' is an encrypted private key, ansible can work with it via the `credentials.yml` file.

To launch ansible with the ability to unlock the encrypted file, add `--ask-vault-pass` to the launch command.

The encrypted file can be replaced with a clear text key, in such case launching ansible with `--ask-vault-pass` is unnecessary-

To modify the file, position yourself in `Ansible` and use the command `ansible-vault edit credentials/id_rsa`.

To replace the key with your own encrypted key, copy your key file inside credentials and launch `ansible-vault encrypt credentials/filename`

## Run the playbook

It is the core component of this configuration, it contains all the tasks that are going to be performed and more environment specific options.

Change directory into `Ansible` folder, then update the `inventory.ini` file with the actual IP addresses of the target machines.

Then launch the playbook for the load balancers:

```bash
ansible-playbook loadBalancer.yml
```

 <strong>Note</strong>: if password is required for sudo privileges on the target machine, append the `--ask-become-pass` parameter to the command above

And the playbook for the webservers:

```bash
ansible-playbook webServer.yml --ask-vault-pass
```
 <strong>Note</strong>: if password is required for sudo privileges on the target machine, append the `--ask-become-pass` parameter to the command above

As stated previously, remove `--ask-vault-pass` if you are not using any encrypted file.

You can limit your run to one or more roles or tasks by editing the playbook in this way

```yml
- { role: rolename, tags: "tagname" }
```

and launching the playbook with  ```--tags "tagname"```

```shell
ansible-playbook playbook.yml --ask-become-pass --ask-vault-pass --tags "tagname"
```
