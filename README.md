Role Name
=========

Bootstrap server (common role):
- install useful packages (vim, ntp etc..)
- install fail2ban to prevent brute force on our services
- change root password
- create a user for deployment (default: sysdeploy)
- add ssh public key to sysdeploy
- remove ssh public key to sysdeploy (in case someone left the company)
- disable root login (default: no)

Requirements
------------

- CentOS 6.6

Role Variables
--------------

- name_sysdeploy: username of the user you will use to manage your server (default: sysdeploy)
- password_root: password hash (default: sysadmin)
- password_sysdeploy: password hash (default: sysdeploy)
- disable_rootlogin: disable root login in sshd (default: no)

Note:
  - Generate your password with: python -c "import crypt, getpass, pwd; print crypt.crypt('putyourpasswordhere', '\$6\$saltsalt\$')"
    For security reason you should overwrite this with your password and encrypt the file with ansible-vault

  - Move your ssh public key from add_keys to remove_keys to automatically remove it from sysdeploy on next ansible-playbook run.

  ** Be sure to be able to login with some user before you disable root ssh login **

Dependencies
------------

No dependencies

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: common, tags: ['common','bootstrap']  }

License
-------

GPLv2

Author Information
------------------

James HORLEY
