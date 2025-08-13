Role Name
=========

A role for patching Ansible Automation Platform following the practices outlined [here](https://access.redhat.com/solutions/7034370).

For best results, use this role with your AAP Installation inventory file.  If you do not have your inventory file, you will need to recreate it as this role uses variables from the installer's inventory file.

If you installed the containerized version of AAP you will need to run the playbook with the same user account you used to install AAP.  And that user will need sudo access to the AAP servers to install updates.

This role will:
- Install dnf-utils (required for reboot check)
- Install updates
- Check if kernel patching (kpatch) is enabled
- If not kpatch, check if reboot is required
- If reboot is required, will disable all AAP Controller and Execution node Instances
- If reboot is required, will wait for all jobs to complete (default wait up to 15 minutes)
- Reboot if reboot was required
- After reboot, will re-enable all AAP Controller and Execution node Instances
- Optional (see vars below) will check Satellite for missing errata
- Optional (see vars below) will refresh RHEL insights-client data.


Requirements
------------

Uses the aap_svc_control role in this collection.
Also will use the redhat.satellite collection if `uses_satellite` is set to `true`

Role Variables
--------------

|Variable Name|Default Value|Required|Type|Description|
|:---:|:---:|:---:|:---:|:---:|
|only_security|false|false|bool|Set to true if you only want to install security updates|
|only_bugfixes|false|false|bool|Set to true if you only want to install bugfixes|
|uses_satellite|false|false|bool|If using satellite and want to check for missing errata, set to true|
|satellite_validate_certs|false|false|bool|If using Satellite, whether to validate SSL certificate of your Satellite server|
|satellite_host|''|false|str|Hostname of your Satellite server|
|satellite_user|''|false|str|Username for connecting to Satellite to check for missing errata|
|satellite_passwd|''|false|str|Password for satellite_user|
|refresh_insights|false|false|bool|If you wish to refresh insights data after patching, set to true|


Dependencies
------------

Uses other roles in this collection.  Also uses redhat.satellite collection for Satellite tasks.

Example Playbook
----------------

The aap.utils collection includes a playbook.  If you installed the containerized version of AAP you will need to run the playbook with the same user account you used to install AAP.  To run the playbook:

For an enterprise topology:\n
`ansible-playbook aap.utils.patch_aap -i inventory`

For a standalone topology:\n
`ansible-playbook aap.utils.patch_aap -i inventory-growth`

For enterprise topology and you want refresh insights data:<br>
`ansible-playbook aap.utils.patch_aap -i inventory -e refresh_insights=true`

For enterprise topology and you want to check for missing errata:<br>
`ansible-playbook aap.utils.patch_aap -i inventory -e uses_satellite=true -e satellite_host=satellte.example.com -e satellite_user=someuser -e satellite_passwd=abcde1234`

For enterprise topology and you want to check for missing errata and refresh insights data:<br>
`ansible-playbook aap.utils.patch_aap -i inventory -e uses_satellite=true -e satellite_host=satellte.example.com -e satellite_user=someuser -e satellite_passwd=abcde1234 -e refresh_insights=true`


License
-------

GPL-3.0-or-later

Author Information
------------------

Tony Reveal (tony.reveal@redhat.com)
