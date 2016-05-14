# amanda

* Step 1:卸载当前已经安装的amanda

	yum erase amanda-backup_server-3.3.8-1.rhel7.x86_64 -y
	yum erase amanda-backup_client-3.3.8-1.rhel7.x86_64 -y
	rm -rf /etc/amanda /amandaback /dumps
	rm -rf /var/log/amanda /var/lib/amanda
	find /|grep amanda|xargs rm -rf

* Step 2:备份服务器端安装amanda-server
	yum localinstall amanda-backup_server-3.3.8-1.rhel7.x86_64.rpm -y
	cp -rf amanda.conf.main /etc/amanda
	chown warm:disk /etc/amanda/amanda.conf.main
	su - warm
	cp /var/lib/amanda/.amandahosts .
	cp /var/lib/amanda/.am_passphrase .
	exit

* Step 3:虚拟机里安装amanda-client
	yum localinstall amanda-backup_client-3.3.8-1.rhel7.x86_64.rpm -y

# Release Notes
* 调整的amanda默认的管理员用户为warm
* 调整了.amandahosts的鉴权