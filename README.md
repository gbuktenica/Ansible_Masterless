# Run Ansible Master-less

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Copyright Glen Buktenica](https://img.shields.io/badge/Copyright-Glen_Buktenica-blue.svg)](http://buktenica.com)

This guide shows how to run an Ansible playbook without using a remote Ansible AWX server, similar to Puppets Master-less mode. This is done by installing Ansible on the target and running **ansible-playbook** locally.

Action the following quick start on a non-production linux server.

## Quick Start

1. Install Ansible

```bash
yum install ansible -y
```

2. Create a playbook.yml

Write the content below to playbook.yml.

```yaml
---
- name: Write File
  hosts: 127.0.0.1
  connection: local
  become: true
  tasks:
    copy:
      content: "test content"
      dest: /home/test
      force: n
```

The above playbook will write a file to
/home/test
with **test content** as the content of the file.

3. Run the following

```bash
ansible-playbook playbook.yml
```

4. Expected Result

The following should be displayed.

```bash
 [WARNING]: provided hosts list is empty, only localhost is available. Note
that the implicit localhost does not match 'all'


PLAY [write file] **************************************************************

TASK [Gathering Facts] *********************************************************
ok: [localhost]

TASK [Write test file] *********************************************************
changed: [localhost]

PLAY RECAP *********************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```

The test file should be created:

```bash
cat /home/test
```

```bash
> test content
```