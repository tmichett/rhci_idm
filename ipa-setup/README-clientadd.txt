Adding clients to IPA.

If you need to log into thos IPA system to make changes manually, the
admin account password is in create_client.yml.

It's a two step process outlined in create_client.yml.

1) On IPA server, set up an account to register to with a one-use password.
2) On the host, ipa-client-install using that password.  If you mess up,
   you'll need to redo the password on the IPA server for that host account.

These hosts will be *registered* to IPA, but until they're placed into a
hostgroup they won't show up in the dynamic inventory.

The actual playbook doesn't work with my current Vagrant setup, but I expect
it to work in a Tower deployment that has credentials set up properly.

