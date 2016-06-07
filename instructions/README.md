# Navodila za instalacijo Ansible s podporo za omrezne naprave

## Priprava virtualnega streznika na VirtualBox
V prvi fazi je potrebno pripraviti virtualni streznik, na katerem se bo izvajal Ansible.

Za instalacijo sledite navodilom:
- Prenesi Ubuntu 14.04 s spletnega mesta - [prenos](http://releases.ubuntu.com/14.04/ubuntu-14.04.4-server-amd64.iso)
- Kreiraj virtualni streznik z naslednjo konfiguracijo:
-- CPU: 1
-- RAM: 2GB
-- Disk: 15GB
-- NIC: 
--- eth0: Attached to NAT
--- eth1: Attached to Host-only Adapter
- Instaliraj Ubuntu
- Nastavi staticni IP na vmesnku eth1
```
# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	# Izberi poljuben IP iz subneta dolocenega za vmesnik
	address 192.168.35.120
	netmask 255.255.255.0
```
- Ponovno zaceni streznik
- Izvedi
```
sudo apt-get update
```

## Instalacija Ansible
- Prenesi Ansible network
```
wget http://releases.ansible.com/ansible-network/2.0.1.0-0.2/ansible_2.0.1.0-0.2.networkppa~trusty_all.deb
```
- Instaliraj Ansible network
```
sudo dpkg -i ansible_2.0.1.0-0.2.networkppa~trusty_all.deb
sudo apt-get -f install
```
- Preveri delovanje ansible
```
$ansible --version
ansible 2.0.1.0
  config file = /etc/ansible/ansible.cfg
  configured module search path = Default w/o overrides
```

  
