# variable<sup>1</sup>

##Introduction

Ansible has great support for variables, allowing you to use them both in playbooks and in files that are copied to the remote machine. 

Variables in Ansible are global. Variables in a role are generally prefixed with the role name. 

## Variable Locations

Not only can they be used in playbooks or files, but you can also define them in sixteen different locations!

Role defaults have the lowest precedence when it comes to setting variable values and are overridden by everything else.

### 1. Role Defaults (Commonly Used)

This is the defaults/main.yml file in your role. Variables set in this file have the lowest precedence of any variables set, which makes it perfect for setting default values.

### 2. Inventory Variables

Most of the time you’ll only use inventory-specific variables in the inventory file (such as ansible_user or ansible_ssh_private_key-file), but you can set any variable you like.

You can also specify variables for a group of hosts or a group of groups, such as:

```ini
[app]
192.168.33.20
192.168.33.21

[app:vars]
your_name=World
```

### 3. Inventory Group Variables

To use inventory group variables, you must create a folder called *inventory/group_ vars*, which can contain variable files for any groups that you have created, such as with the following *inventory/inventory* file:

```yaml
[app]
192.168.33.20
192.168.33.21

[admin]
192.168.33.33

[database]
192.168.33.55
```

To specify group variables for the hosts in this inventory file, you must have a folder structure that looks like that:

```shell
inventory
	group_vars
		admin.yml
		app.yml
		database.yml
	inventory
```

Any variables that you define in *inventory/group_vars/admin.yml* will be available on any hosts in the admin group.

### 4. Inventory Host Variables

Similar to *inventory/group_vars*, you can specify variables per host.

You can create a folder structure that looks like that:

```
inventory
	host_vars
		192.168.33.20.yml
		192.168.33.21.yml
	inventory
```

### 5. Playbook Group Variables (Commonly Used)

Group variables can also be defined at the playbook level in a *group_vars* folder. They look and behave exactly like the inventory group_vars folder, except that they are at the same level as playbook.yml and have a slightly higher precedence.

### 6. Playbook Host Variables (Commonly Used)

Just like group variables, host variables can be defined at the playbook level. They’re functionally equivalent to the inventory host_vars, but with a slightly higher precedence.

### 7. Host Facts

Ansible has the concept of a “fact,” which is information that is available about the current host. These facts exist during an Ansible run as variables for you to use in your playbooks and templates.

When Ansible runs, it runs the setup module to gather facts about a host. If you define facts with the same names as role defaults or group or host variables, they will be overwritten with the host facts. If you register a variable or use the set_fact module using the same name as a built-in fact, the host fact will be overwritten. All facts are prefixed with ansible_, so it is difficult to overwrite them accidentally.

To see which facts are available for a host, you can use the setup module as follows:

```shell
ansible all –i /path/to/inventory –m setup
```

### 8. Registered Variables (Commonly Used)

When working within a playbook, you may want to save the output from modules.

```yaml
---
- hosts: all
  tasks:
	- stat: path=/etc/hosts
	  register: hosts_info
	- debug: var=hosts_info
```

### 9. Set Facts

```yaml
---
- hosts: all
  tasks:
	- set_fact: example_var="Hello world"
	- debug: var=example_var
```

It only really starts to become useful when you need to manipulate the results of another module call in a playbook.

### 10. Playbook Variables

You can set variables directly in a playbook. To define variables in a playbook, you just create a *vars* section at the same level as tasks.

```yaml
---
- hosts: all
  gather_facts: false
  vars:
  	your_name: World
  tasks:
  	- debug: msg="Hello {{your_name}}"
```

###11. Playbook vars_prompt

When running a playbook, there may be information that you need to collect at runtime. This may be sensitive information, such as passwords.

```yaml
--
- hosts: all
  vars_prompt:
  	- name: your_name
  	  prompt: "What is your name?"
  tasks:
  	- debug: msg="Hello {{your_name}}"
```

### 12. Playbook vars_files

Playbooks will read group_vars and host_vars by default, but you can also instruct them to read additional variable files via the vars_files parameter in a playbook.

```yaml
---
- hosts: all
  vars_files:
  	- michael.yml
  tasks:
  	- debug: msg="Hello {{your_name}} from {{location}}"
```

This playbook will load michael.yml in the same folder. If it doesn’t exist, you will get an error. You can provide defaults for vars_files, and Ansible will include the first one that it finds.

```yaml
---
- hosts: all
  vars_prompt:
	- name: include_file
	  prompt: "Which file should we include?"
  vars_files:
  	- ["{{include_file}}.yml", "default_user.yml"]
  tasks:
  	- debug: msg="Hello {{your_name}} from {{location}}"
```

### 13. Role Variables (Commonly Used)

When using roles in a playbook, you can specify variables that should be used when running that role.

```yaml
---
- hosts: all
	become: true
	roles:
		- role: mheap.wordpress
		database_name: michaelwp
		database_user: michaelwp
		database_password: bananas18374
```

> The copy module doesn’t do anything to the file—it just copies it as is. To have your variables populated, you’ll need to use the template module instead.

### 14. Block Variables

A block in Ansible is a grouping of tasks. Instead of specifying become and when for every task in this example, you can use a block and specify it once for all tasks inside that block.

```yaml
- hosts: all
  tasks:
  	- block:
  		- apt: name=apache2 state=installed
  		- copy: content="Example File" dest=/var/www/hello.html
  		become: true
  		when: do_something.rc == 0
```

### 15. Task Variables

In addition to block-level variables, you can specify variables at a per-task level.

```yaml
- hosts: all
  tasks:
  	- debug: msg="Hello {{your_name}}"
  	  vars:
  		your_name: Michael
```

### 16. Extra Variables

Extra variables are specified at runtime and have the highest priority of all variables set.

```shell
ansible-playbook –i /path/to/inventory playbook.yml –e 'your_name=Fred'
```

You can specify multiple –e flags to set as many variables as you like.

If you have lots of additional variables, you may prefer to pass a filename that will be read instead:

```shell
ansible-playbook –i /path/to/inventory playbook.yml –e @large_variable_ file.json
```



***

## Ansible’s Variable Philosophy

You can define variables at various levels throughout an Ansible playbook, but Ansible’s philosophy is that a variable should usually be defined only once.

Most of the time, however, you’ll only be setting it in one of the common locations.



***

1. From *Ansible From Beginner to Pro*