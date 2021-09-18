[![Ansible Galaxy](https://raw.githubusercontent.com/roles-ansible/ansible_role_users/main/.github/galaxy.svg?sanitize=true)](https://galaxy.ansible.com/do1jlr/users) [![MIT License](https://raw.githubusercontent.com/roles-ansible/ansible_role_users/main/.github/license.svg?sanitize=true)](https://github.com/roles-ansible/ansible_role_users/blob/main/LICENSE)

 ansible_role_users
==============================
Ansible role to create admin and non-admin users on linux hosts.

 intended use
---------------
This role is designed to manage linux hosts with the following roles. This role here basically only focuses on creating users and giving them admin rights depending on the configuration.
Other roles distribute ssh public keys, configure sshd, roll out dotfiles or install a number of useful packages.

A list of suggested roles to manage your linux host:
 - [do1jlr.base](https://github.com/roles-ansible/ansible_role_base.git) *install some useful packages*
 - [do1jlr.users](https://github.com/roles-ansible/ansible_role_users.git) *(this one)*
 - [do1jlr.auth](https://github.com/chaos-bodensee/role-ssh_authorized_keys.git) *deploy ssh pubkeys*
 - [do1jlr.sshd](https://github.com/roles-ansible/ansible_role_sshd.git) *configure sshd*
 - [do1jlr.dotfiles](https://github.com/roles-ansible/ansible_role_dotfiles) *deploy some fancy dotfiles*

 Good to know:
---------------
The listed roles use the same variables to create accounts, admins and so on. But the roles have to run in the correct order to work properly.
For example you can't deploy a ssh public key for a user that is not created.

 Variables
---------

* ``admins`` (default ``[]``):<br/>
  A list of ``ssh`` keys allowed to log in as `root`.

* ``accounts`` (default ``[]``):<br/>
  A list of usernames that will be created on this host, if they don't exisit

* ``default shell`` (default ``/bin/bash``)


* ``manage_user_passwords`` (default ``false``)
  manage user passwords?

* ``accounts_with_password`` (default ``[]``)
  all users and password hashes

For aditional variables please have a look into ``defaults/main.yml``!


 Examples
--------

Alice and Bob may log in and are allowed to become ``root`` with the ``sudo`` command on this host:

```
admins:
  - alice
  - bob
```

Alice, Bob and Eve want to be users on this host:
```
# without password
accounts:
  - alice
  - bob
  - eve

# with password
accounts_with_password:
  alice:
    - "$6$foo$LtJkKZx0ndF4kM0ImEtCaQhbMYWD.mlqatgAIzuDufGI0IGxe0wpSV7oXqwnLmO4MA.4A5JCnPhOqUyT3OfVV1"
  bob:
    - "$6$bar$fsDFaQrp1MI9yhNnoKlXJFfXSLpz/dpqWaA2NP/71WJUzfqQxPVvFY6Px7VlDppW/NB6Cbz6BjF2b9bD.riFX1"
  eve:
    - "$6$baz$7xpdAhdFpIM304YYQ88nz33xmJXnh5qxtlWoGSkc55a.R4DCRp62l.qhiYKbtjRzEjb5qnGoM9vthcHagPkyS/"
```
### Protipp:
Use this to generate a password hash. *(Obviously you have to replace``MyPassword`` with your password!)*
```
python3 -c 'import crypt; print(crypt.crypt("MyPassword"))'
```
