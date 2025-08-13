AAP_SVC_CONTROL
=========

A role to stop, start, or restart AAP 2.5, utilizing the AAP 2.5 installation inventory file.

If you do not have your Automation Platform installation inventory file, you will need to recreate it as this role uses variables from the installer's inventory file.

If you installed the containerized version of AAP you will need to run the playbook with the same user account you used to install AAP.

Requirements
------------

Primarily uses the `ansible.builtin` collection but also requires the `ansible.controller` collection.

Role Variables
--------------

| Variable Name | Default Value | Required | Type | Description |
| :---: | :--- | :---: | :---: | :---: |
|desired_state|restarted|false|str|The operation you wish to perform. Accepted values are `stopped`, `started`, and `restarted`|
|aap_validate_certs|false|false|bool|Whether or not to validate AAP certs when getting a token or disabling/enabling instances.|

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

The aap.utils collection includes a playbook.  If you installed the containerized version of AAP you will need to run the playbook with the same user account you used to install AAP.  To run the playbook:

For an enterprise topology:
`ansible-playbook aap.utils.aap_svc_ctrl -e desired_state=restarted -i inventory`

For a standalone topology:
`ansible-playbook aap.utils.aap_svc_ctrl -e desired_state=restarted -i inventory-growth`

License
-------

GPL-3.0-or-later

Author Information
------------------

Tony Reveal (tony.reveal@redhat.com)
