 role ssh_authorized_keys
==============================
Ansible Rolle to manage and deploy ssh keys of admin and non-admin users

 combinations
---------------
It is highly recomended to use this role together with a role to manage users and to manage the sshd configuration.<br/>
The following roles are tested in combination and work well - at least for the user [DO1JLR](https://github.com/do1jlr):
 - [github.com/chaos-bodensee/role-manage_users](https://github.com/chaos-bodensee/role-manage_users.git) *(this one)*
 - [github.com/chaos-bodensee/role-ssh_authorized_keys](https://github.com/chaos-bodensee/role-ssh_authorized_keys.git)
 - [github.com/chaos-bodensee/role_sshd](https://github.com/chaos-bodensee/role_sshd.git)

```txt
Protipp:

Deploy the manage_users role *before* deploying the ssh keys.
If the user does not exist it is hard to add a ssh key for him!
```

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
