# DirectAdmin-1.59.5 - Installation Successful
# P/s: Chú ý bản này chỉ chạy được trên Centos 7 64bit
# Cài đặt:
```
 yum -y install nano wget perl
 wget https://raw.githubusercontent.com/akkradet/DirectAdmin-1.59.5/master/setup.sh
 chmod +x setup.sh
 ./setup.sh
```
# Enter the ID and LICID any number you like.

# Note that after installation will not run, declare port for it commands:
```
firewall-cmd --zone=public --add-port=2222/tcp --permanent
firewall-cmd --zone=public --add-port=21/tcp --permanent
firewall-cmd --zone=public --add-port=80/tcp --permanent
firewall-cmd --zone=public --add-port=25/tcp --permanent
firewall-cmd --reload
systemctl restart directadmin
cd /usr/local/directadmin/conf/
service directadmin stop
rm -rf /usr/local/directadmin/conf/license.key
wget -O /usr/local/directadmin/conf/license.key https://raw.githubusercontent.com/akkradet/DirectAdmin-1.59.5/master/license.key
chmod 600 /usr/local/directadmin/conf/license.key
chown diradmin:diradmin /usr/local/directadmin/conf/license.key
ifconfig eth0:100 103.127.207.212 netmask 255.0.0.0 up
echo 'DEVICE=eth0:100' >> /etc/sysconfig/network-scripts/ifcfg-eth0:100
echo 'IPADDR=103.127.207.212' >> /etc/sysconfig/network-scripts/ifcfg-eth0:100
echo 'NETMASK=255.0.0.0' >> /etc/sysconfig/network-scripts/ifcfg-eth0:100
service network restart
/usr/bin/perl -pi -e 's/^ethernet_dev=.*/ethernet_dev=eth0:100/' /usr/local/directadmin/conf/directadmin.conf
service directadmin start
ifdown eth0:100
```
# If the license expires (read commit new update term), then simply run the following command:
# IF IPADDR in /etc/sysconfig/network-scripts/ifcfg-eth0:100 != 103.127.207.212 then EDIT TO 103.127.207.212

```
rm -rf /usr/local/directadmin/conf/license.key
wget -O /usr/local/directadmin/conf/license.key https://raw.githubusercontent.com/akkradet/DirectAdmin-1.59.5/master/license.key
chmod 600 /usr/local/directadmin/conf/license.key
chown diradmin:diradmin /usr/local/directadmin/conf/license.key
ifup eth0:100
systemctl restart directadmin
ifdown eth0:100
```
# How to fix VPS not on network after edit network:

```ifdown eth0:100```
