AAP Preinstall Checks
=========

This role will verify these basic minimum requirements have been met to install Automation Platform 2.5.  To use this role you will need to use your populated AAP installation inventory file.

If you do not populated your Automation Platform installation inventory file, you will need to do so before using this role as this role uses variables from the installer's inventory file.

If you plan to install the containerized version of AAP you will need to run the playbook with the same user account you used to install AAP.  Sudo privileges may be required to run the content in this role but should not be required to install containerized AAP.

  Common:
    - min 4 CPU
    - min 16 GB RAM
    - umask
    - UID
    - firewalld status
    - default firewalld zone

  AAP containerized:
    - free space on `/home`
    - free space on `/tmp`
    - port connectivity tests
        - HTTPS
        - Receptor
        - Redis
        - PostgreSQL
    - validate postgresql vars
    - external database login test
    - NFS Mount if more than 1 host in automationhub hostgroup
        - /home/<user>/aap/hub/data
    - Is installing user a local or domain user?
        - if domain user - check /etc/subuid and /etc/subgid <-- Not yet implemented

  AAP rpm:
    - free space on `/var`
        - or `/` if `/var` is not a mount point
    - port connectivity tests
        - HTTPS
        - Receptor
        - Redis
        - PostgreSQL
    - validate postgresql vars
    - external database login test
    - NFS Mount if more than 1 host in automationhub hostgroup
        - /var/lib/pulp

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
