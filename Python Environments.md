# Python Environments

## Introduction

Because Python was being actively developed, users often complained that they would like to use a more up-to-date version of the language than their operating system provided. Techniques arose to let multiple versions of the language be installed on a system

Installation of third-party software remained nonstandard and intrusive. This problem was eased by the introduction of the site-packages directory as the repository for modules added to a Python installation.

But, it was still not possible to maintain projects with conflicting requirements using the same interpreter.

Various aspects of the shell environment affect Python’s operation. Those aspects of your shell environment that affect Python’s operation are as your Python environment.

## Enter the Virtual Environment

That is just what virtual environments (virtualenvs) give you the ability to make controlled changes to the Python environment, to direct the use of a specific interpreter and a specific set of Python libraries.

Creating a virtualenv based on a specific Python interpreter copies or links to components from that interpreter’s installation. Each one has its own site-packages directory.

A typical newly created virtualenv takes less than 20 MB.

You can activate and deactivate a virtualenv as many times as you like during its lifetime.

When you are done with it, removing its directory tree reclaims all storage occupied by the virtualenv.

## What is a Virtual Environment?

A python interpretor with every stand-alone site-packages directory.

For a Python X.Y interpreter it includes, among other things, a **bin directory** containing a Python X.Y interpreter and a **lib/ pythonX.Y/site-packages** directory containing preinstalled versions of easyinstall, pip, pkg_resources, and setuptools.

A virtualenv has its own copies of (on Windows), or **symbolic links to** (on other platforms), Python distribution files. It adjusts **the values of sys.prefix and sys.exec_prefix**, from which the interpreter and various installation utilities determine the location of some libraries.

In effect the virtualenv redefines which interpreter runs when you run the python command and which libraries are available to it.

With separate virtualenvs you can, for example, **test two different versions of the same library** with a project, or **test your project with multiple versions of Python**. You can also **add dependencies to your Python projects without needing any special privileges**, since you normally create your virtualenvs somewhere you have write permission.

For a long time the only way to create virtual environments was the **third-party virtualenv package**, **with or without help from virtualenvwrapper**, both of which are still available for v2. They also work with v3, but the 3.3 release added **the venv module**, making virtual environments a native feature of Python for the first time.

## Creating and Deleting Virtual Environments

**In v3** the command `python -m venv envpath` creates a virtual environment (in the envpath directory, which it also creates if necessary) based on the Python interpreter used to run the command.

**v2** users must use the `python -m virtualenv command`, which does not accept multiple directory arguments.

Deletion of the virtualenv is as simple as removing the directory in which it resides.

The venv module includes features to help **the programmed creation** of tailored environments

## Working with Virtual Environments

To use a virtualenv you **activate it from your normal shell** environment.

**Only one virtualenv can be active** at a time—activations don’t “stack” like function calls.

When you want to stop using those dependencies, **deactivate the virtualenv** and your standard Python environment is once again available

The **virtualenv directory tree continues to exist until deleted**, so you can activate and deactivate it at will.

Activating a virtualenv **in Unix-based environments** requires use of the `source` shell command so that **the commands in the activation script** make changes to the current shell environment.

**Simply running the script would mean its commands were executed in a subshell**, and the changes would be lost when the subshell terminated.

For bash and similar shells:

> `source envpath/bin/activate`

Activation does several things, most importantly:

> - Adds the virtualenv’s bin directory at the beginning of the shell’s PATH environment variable
> - Defines a deactivate command
> - Modifies the shell prompt to include the virtualenv’s name at the start
> - Defines a VIRTUAL_ENV environment variable

Those new to virtualenvs should understand that a virtualenv is not tied to any project directory. It’s perfectly possible to work on several projects, each with its own source tree, using the same virtualenv. Activate it, then move around your filestore as necessary to accomplish your programming tasks, with the same libraries available (because **the virtualenv determines the Python environment**).

When you want to disable the virtualenv and stop using that set of resources, simply issue the command `deactivate`.

## Managing Dependency Requirements

Since virtualenvs were designed to complement installation with pip, it should come as no surprise that **pip is the preferred way to maintain dependencies in a virtualenv**.

To maintain the same set of dependencies in several virtualenvs, use the same **requirements file** to add dependencies to each one.

`pip install -r <requiement file>`

This is a convenient way to develop projects to run on multiple Python versions: create virtualenvs based on each of your required versions, then install from the same requirements file in each.

## Best Practices

**There is remarkably little advice** on how best to manage your work with virtualenvs, though there are several sound tutorials: any good search engine gives you access to the most current ones. We can, however, offer a modest amount of advice that we hope will help you to get the most out of them.

When you are working with the same dependencies in multiple Python versions, **it is useful to indicate the version in the environment name** and use a common prefix. So for project mutex you might maintain environments called mutex_35 and mutex_27 for v3 and v2 development. When it’s obvious which Python is involved (and remember you see **the environment name in your shell prompt**), there’s less chance of testing with the wrong version. You maintain dependencies using common requirements to control resource installation in both.

**Keep the requirements file(s) under source control, not the whole environment**. Given the requirements file it’s easy to re-create a virtualenv, which depends only on the Python release and the requirements. You distribute your project, and let your consumers decide which version(s) of Python to run it on and create the appropriate (hopefully virtual) environment(s).

Keep your virtualenvs outside your project directories, or you would explicitly force source code control systems to ignore them. It really doesn’t matter where you store them—the virtualenvwrapper system keeps them all in a central location.

Your Python environment is independent of your process’s location in the filesystem. You can activate a virtual environment and then switch branches and move around a change-controlled source tree to use it wherever convenient.

---

1. Reference: <Python in a Nutshell v3>

