# amanda

* Step 1:uninstall existed amanda
```
// bash
yum erase amanda-backup_server-3.3.8-1.rhel7.x86_64 -y
yum erase amanda-backup_client-3.3.8-1.rhel7.x86_64 -y
rm -rf /etc/amanda /amandaback /dumps
rm -rf /var/log/amanda /var/lib/amanda
#find /|grep amanda|xargs rm -rf
```

* Step 2:backup server install amanda-server
```
// bash
yum localinstall amanda-backup_server-3.3.8-1.rhel7.x86_64.rpm -y
cp -rf amanda.conf.main /etc/amanda
chown warm:disk /etc/amanda/amanda.conf.main
su - warm
cp /var/lib/amanda/.amandahosts .
cp /var/lib/amanda/.am_passphrase .
exit
```
* Step 3:install amanda-client to vm
```
// bash
yum localinstall amanda-backup_client-3.3.8-1.rhel7.x86_64.rpm -y
```
# Release Notes

* change amanda default admin to warm

* change .amandahosts policy