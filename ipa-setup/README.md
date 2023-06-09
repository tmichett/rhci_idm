= ipa-setup

Main playbooks in this Ansible project:

  - create_ipa_server.yml
    Main playbook for configuring utility.lab.example.com with FreeIPA
    Admin password is in the playbook
    Not idempotent.

    You can 'kinit -f admin' with the admin password and then use the
    'ipa' command to manage the server from the CLI.

    It may make sense to update this to also setup DNS for lab.example.com
    and then forward to the classroom DNS server, but that's not been tried.

  - create_client.yml
    Main playbook for registering clients.  Not fully tested but the
    outline of the procedure is sound.
    Not idempotent.

Supplementary drafts

  - create_ipa_server_hostgroups.yml was a test book to just set up hostgroups
  - delete_ipa_server_hostgroups.yml to reverse that
  - remove_client.yml to unregister a client, not well tested (not sure is
    even the right procedure)


== LDAP Modules for python

Need to install python3-ldap on Workstation machine
