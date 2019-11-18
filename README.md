# C106-2017

Ansible Automation

## Requirements

**Manager node:**

- Ubuntu 18.04
- Python Python 2.7.15
- SSH
- Ansible 2.9

**Managed nodes:**

- Ubuntu 18.04
- SSH

## Environment setup

Ansible by default manages machines over SSH and assumes SSH keys are being used.
Ansible only needs to be installed on a machine to be able to manage other machines and it doesn't leave software installed or running on managed machines.

### Install the latest version via pip

Install the Python package manager

```sh
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python get-pip.py --user
```

Then install ansible

```sh
pip install --user ansible
```

## Credentials

The purpose of the credentials folder is to store sensitive data. The file 'id_rsa' is an encrypted private key, ansible can work with it via the `credentials.yml` file.

To launch ansible with the ability to unlock the encrypted file, add `--ask-vault-pass` to the launch command.

The encrypted file can be replaced with a clear text key, in such case launching ansible with `--ask-vault-pass` is unnecessary-

To modify the file, position yourself in `Ansible` and use the command `ansible-vault edit credentials/id_rsa`.

To replace the key with your own encrypted key, copy your key file inside credentials and launch `ansible-vault encrypt credentials/filename`

