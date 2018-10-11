# usermod

## Motivation

On CentOS, I need to grant a user *root privilege*, which was created before.

## Introduction<sup>1</sup>

The *usermod* command modifies the system account files<sup>2</sup> to reflect the changes that are specified on the command line.

## Useful Options

***
-a, --append

> Add the user to the supplementary group(s). Use only with the -G option.

-G, --groups GROUP1[,GROUP2,...[,GROUPN]]]

> A list of supplementary groups which the user is also a member of. Each group is separated from the next by a comma, with no intervening whitespace.

Example:

> `usemod -a -G <user group> <user name>` would add a specified user to the group.


***
1. *From man page*.

2. *What files are system account files?*

