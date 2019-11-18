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

