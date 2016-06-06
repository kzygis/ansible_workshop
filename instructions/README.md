# Navodila za instalacijo Ansible s podporo za omrezne naprave

## Priprava virtualnega streznika na VirtualBox
V prvi fazi je potrebno pripraviti virtualni streznik, na katerem se bo izvajal Ansible.

Za instalacijo sledite navodilom:
- Prenesi Ubuntu 14.10 s spletnega mesta - [prenos](http://old-releases.ubuntu.com/releases/utopic/ubuntu-14.10-server-amd64.iso)
- Kreiraj virtualni streznik - [screenshoot1](https://raw.githubusercontent.com/ubajze/ansible_workshop/master/instructions/sc/sc1.png)
- Dodeli RAM (2GB) - [screenshoot2](https://raw.githubusercontent.com/ubajze/ansible_workshop/master/instructions/sc/sc2.png)
- Kreiraj virtualni disk - [screenshoot3](https://raw.githubusercontent.com/ubajze/ansible_workshop/master/instructions/sc/sc3.png) [screenshoot4](https://raw.githubusercontent.com/ubajze/ansible_workshop/master/instructions/sc/sc4.png) [screenshoot5](https://raw.githubusercontent.com/ubajze/ansible_workshop/master/instructions/sc/sc5.png) [screenshoot6](https://raw.githubusercontent.com/ubajze/ansible_workshop/master/instructions/sc/sc6.png)
- Dokoncaj pripravo virtualnega streznika
- Pojdi v nastavitve virtualnega streznika
- Izberi mrezne nastavitve
- Izberi prvi mrezni adapter in ga nastavi kot NAT - [screenshoot7](https://raw.githubusercontent.com/ubajze/ansible_workshop/master/instructions/sc/sc7.png)
- Izberi drugi mrezni adapter in ga nastavi kot Host-only Adapter [screenshoot8](https://raw.githubusercontent.com/ubajze/ansible_workshop/master/instructions/sc/sc8.png)
- Izberi zavihek Storage in v opticni pogon dodaj ISO datoteko, ki si jo prenesel v prvem koraku - [screenshoot9](https://raw.githubusercontent.com/ubajze/ansible_workshop/master/instructions/sc/sc9.png) [screenshoot10](https://raw.githubusercontent.com/ubajze/ansible_workshop/master/instructions/sc/sc10.png)
- Instaliraj Ubuntu [screenshoot11](https://raw.githubusercontent.com/ubajze/ansible_workshop/master/instructions/sc/sc11.png) 
- Nastavi staticni IP na vmesnku eth1 (/etc/network/interfaces)
```
# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.168.35.120
	netmask 255.255.255.0
```
- Ponovno zaceni streznik



-  
