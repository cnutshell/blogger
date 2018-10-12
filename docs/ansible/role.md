#Role<sup>1</sup>

## Introduction

*role* makes playbooks reusable.

Playbooks and role are very similar. A playbook is a standalone file that ansible can run that contains all the information required to set a machine's state to what you expect. A playbook can contain variables, tasks, handlers, roles, and even other playbooks.

**You can think a role as a playbook that is split up into multiple different files.** There’s one file for variables, one for tasks, and another for handlers. You can’t run a role on its own, though; you need to include it inside a playbook along with the information about which hosts to run on.

**Roles are the mechanism that you use to package up tasks, handlers, and everything else that you need into reusable components.**

## Get a Role

You should run the `ansible-galaxy` command in the same directory where playbook.yml can be found.

## Use a Role

```yaml
---
- hosts: all
  roles:
  	- geerlingguy.git
```

## Role Structure

Using the ansible-galaxy command-line tool, you can create a new role in your roles folder.

```shell
mkdir -p provisioning/roles
cd provisioning/roles
ansible-galaxy init mheap.php
```

Role names are generally in the form <identifier>.<rolename>; for example, geerlingguy.git.

The init command will create a folder called mheap.php, which contains all of the possible files for an Ansible role.

```shell
README.md		// Explain the purpose of the role
defaults
	main.yml	// configuration file; define default values for variables
files			// place files cannot be manipulated at all, however, just copied
handlers
	main.yml	// define handlers
meta
	main.yml	// define the metadata that Ansible Galaxy uses if you publish your module
tasks
	main.yml	// This is the tasks section that was in your playbook
templates		// place template files
tests			// place test playbooks that consume your role
	inventory
	test.yml
vars
	main.yml	// define variables that will override anything in defaults/main.yml
```

Most of the folders created are optional. Most of the time, you’ll find that you’re working in the tasks folder, with supporting files found in handlers and templates.

*main.yml* is the file name that Ansible loads when including a role. You can create new files alongside it in the folder and include those files in main.yml. You need to tell Ansible that these files exist, which you do by editing main.yml so that it looks like the following:

```yaml
---
- include: 'php.yml'
- include: 'extensions.yml'
```

## Role Dependencies

You can use that to specify a role’s dependencies and have Ansible include them for you automatically.

```yaml
dependencies:
	- mheap.common
	- mheap.php
	- mheap.mysql
	- mheap.nginx
```

Ansible parses the metadata for each role it encounters and ensures that any dependencies listed are run before that role.

## Wrapper Roles

If you set a default value for a variable in your role. you can change the name in your wrapper roles to overrides it.



***

1. From *Ansible From Beginner to Pro*
