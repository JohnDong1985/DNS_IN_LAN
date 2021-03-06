# DNS_IN_LAN
* for centos 6.x


## install dnsmasq##
```shell
yum install -y dnsmasq
```

## configure dnsmasq##
```shell
mv /etc/dnsmasq.conf /etc/dnsmasq.conf.bak
touch /etc/dnsmasq.conf
touch /etc/resolv.dnsmasq.conf
touch /etc/dnsmasq.hosts
echo "resolv-file=/etc/resolv.dnsmasq.conf" >> /etc/dnsmasq.conf
echo "addn-hosts=/etc/dnsmasq.hosts" >> /etc/dnsmasq.conf
echo "nameserver 127.0.0.1" > /etc/resolv.conf
echo "nameserver 114.114.114.114" >> /etc/resolv.dnsmasq.conf 
echo "nameserver 8.8.8.8" >> /etc/resolv.dnsmasq.conf 
echo "nameserver 8.8.4.4" >> /etc/resolv.dnsmasq.conf 
echo "x.x.x.x $domain_name1" >>/etc/dnsmasq.hosts 
```

## start dnsmasq##
```shell
service dnsmasq start
```

## check dnsmasq run status##
```shell
netstat -tunlp | grep 53
```

## configure your other host in lan##
```shell
sed -i 's|HOSTNAME=localhost.localdomain|$your_domain_name|g' /etc/sysconfig/network
hostname $your_domain_name 
```

## dns tools for centos##
* bind-utils
* setup and usage
```shell
yum install -y bind-tuils
dig $domain_name
```


* nscd
* setup and usage
```shell
yum install -y nscd
nscd -i hosts
```

## bind your eth0 with a static ip##
* exapmle:
```shell
DEVICE=eth0
TYPE=Ethernet
ONBOOT=yes
NM_CONTROLLED=yes
BOOTPROTO=static
IPADDR=192.168.212.173
GATEWAY=192.168.212.2
BROADCAST=192.168.212.255
NETWORK=192.168.212.0
DNS1=192.168.212.174
```
