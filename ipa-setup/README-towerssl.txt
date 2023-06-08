To set up TLS/SSL on Ansible Tower host.

1) Register the Tower host to the IPA server (we have an untested playbook 
   for this).  Do not assign it to any hostgroups so it won't show up in 
   the dynamic inventory.

2) Generate a key and get a certificate signed by the IPA server's CA.
 
   In real life, what we'd do is

     - Fix the SELinux context on /etc/tower/tower.{cert,key} so that
       they're type cert_t and not etc_t.  (Tower can read this type.)
       You'd want to do
        semanage fcontext -a -t cert_t /etc/tower/tower.cert
        semanage fcontext -a -t cert_t /etc/tower/tower.key
        restorecon -v /etc/tower/*

     - Get the key and cert from IPA with

       ipa-getcert request -f /etc/tower/tower.cert -k /etc/tower/tower.key -r

       The -r would register this certificate with the 'certmonger' service
       running on the system, and the cert would *autorenew* itself from IPA
       when it expired.

     - The alternative plan would be to pull those certs either in 
       advance or to 
          /etc/pki/tls/certs/tower.cert
          /etc/pki/tls/private/tower.key
       and then have students manually copy them in place.

3) As root on Tower, 'ansible-tower-service restart'

4) Test the certificate.  There should be a copy of the IPA server's CA
   certificate for validation at http://utility.lab.example.com/lab/config/ca.crt 
   or in /etc/ipa/ca.crt on registered systems.


