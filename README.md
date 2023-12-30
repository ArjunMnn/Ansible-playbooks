Ansible, an open-source automation tool, is widely used for configuration management, application deployment, and task automation. In this tutorial, we'll explore three common automation tasks using Ansible: creating a file on a different server, creating a new user, and installing Docker on a group of servers. Along the way, we'll also discuss best practices for writing Ansible playbooks.

[](https://arjunmenon.hashnode.dev/day-57-58-ansible-playbooks#heading-prerequisites "Permalink")
-------------------------------------------------------------------------------------------------

Prerequisites
-------------

Before diving into Ansible automation, ensure that you have Ansible installed on your control machine. You can follow the installation instructions on this [blog post](https://arjunmenon.hashnode.dev/day-55-56-configuration-management-with-ansible).

All the code used in this tutorial is available in [this repository](https://github.com/ArjunMnn/Ansible-playbooks).

[](https://arjunmenon.hashnode.dev/day-57-58-ansible-playbooks#heading-task-1-creating-a-file-on-a-different-server "Permalink")
--------------------------------------------------------------------------------------------------------------------------------

Task 1: Creating a File on a Different Server
---------------------------------------------

### [](https://arjunmenon.hashnode.dev/day-57-58-ansible-playbooks#heading-ansible-playbook "Permalink")

### Ansible Playbook

```
---
- name: Create a file on a different server
  hosts: all
  become: true
  tasks:
    - name: Ensure the file exists
      file:
        path: /home/ubuntu/file.txt
        state: touch

```

### [](https://arjunmenon.hashnode.dev/day-57-58-ansible-playbooks#heading-explanation "Permalink")

### Explanation

This playbook is designed to run on all servers specified in the inventory file. The `become: true` directive is used to execute tasks with elevated privileges. The single task, defined under `tasks`, utilizes the `file` module to ensure the existence of the specified file.

[](https://arjunmenon.hashnode.dev/day-57-58-ansible-playbooks#heading-task-2-creating-a-new-user "Permalink")
--------------------------------------------------------------------------------------------------------------

Task 2: Creating a New User
---------------------------

### [](https://arjunmenon.hashnode.dev/day-57-58-ansible-playbooks#heading-ansible-playbook-1 "Permalink")

### Ansible Playbook

```
---
- name: Create a new user
  hosts: all
  become: true
  tasks:
    - name: Create a user with the name ansible-user
      user:
        name: ansible-user

```

### [](https://arjunmenon.hashnode.dev/day-57-58-ansible-playbooks#heading-explanation-1 "Permalink")

### Explanation

This playbook targets all hosts (`all`) and utilizes the `user` module to create a new user named "ansible-user." The `become: true` directive is included to execute the task with elevated privileges.

[](https://arjunmenon.hashnode.dev/day-57-58-ansible-playbooks#heading-task-3-installing-docker-on-a-group-of-servers "Permalink")
----------------------------------------------------------------------------------------------------------------------------------

Task 3: Installing Docker on a Group of Servers
-----------------------------------------------

### [](https://arjunmenon.hashnode.dev/day-57-58-ansible-playbooks#heading-ansible-playbook-2 "Permalink")

### Ansible Playbook

```
---
- name: Install Docker
  hosts: docker_servers
  become: true
  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes
    - name: Install Docker
      apt:
        name: docker.io
        state: present

```

### [](https://arjunmenon.hashnode.dev/day-57-58-ansible-playbooks#heading-explanation-2 "Permalink")

### Explanation

This playbook targets a group of servers (`docker_servers`) to install Docker. The tasks involve updating the APT cache and installing the [`docker.io`](http://docker.io) package using the `apt` module. As before, `become: true` is used to execute tasks with elevated privileges.
