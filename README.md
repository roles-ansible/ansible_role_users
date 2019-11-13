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
accounts:
  - alice
  - bob
  - eve
```

