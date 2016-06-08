# Navodila za instalacijo Ansible s podporo za omrezne naprave

## Priprava virtualnega streznika na VirtualBox
V prvi fazi je potrebno pripraviti virtualni streznik, na katerem se bo izvajal Ansible.

Za instalacijo sledite navodilom:
* Prenesi Ubuntu 14.04 s spletnega mesta - [prenos](http://releases.ubuntu.com/14.04/ubuntu-14.04.4-server-amd64.iso)
* Kreiraj virtualni streznik z naslednjo konfiguracijo:
 * CPU: 1
 * RAM: 2GB
 * Disk: 15GB
 * NIC: 
  * eth0: Attached to NAT
  * eth1: Attached to Host-only Adapter
* Instaliraj Ubuntu
* Nastavi staticni IP na vmesnku eth1
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
* Ponovno zaceni streznik
* Izvedi
```
sudo apt-get update
```

## Instalacija Ansible
* Prenesi Ansible network
```
wget http://releases.ansible.com/ansible-network/2.0.1.0-0.2/ansible_2.0.1.0-0.2.networkppa~trusty_all.deb
```
* Instaliraj Ansible network
```
sudo dpkg -i ansible_2.0.1.0-0.2.networkppa~trusty_all.deb
sudo apt-get -f install
```
* Preveri delovanje ansible
```
$ansible --version
ansible 2.0.1.0
  config file = /etc/ansible/ansible.cfg
  configured module search path = Default w/o overrides
```

## Instalacija Cisco CSR usmerjevalnikov na VirtualBox
* Prenesi brezplacno razlicico CSR 1000v usmerjevalnika iz cisco.com (potreben je vpis z uporabniskim imenom in geslom) - npr. csr1000v-universalk9.03.15.00.S.155-2.S-std.iso
* Kreiraj virtualni streznik z naslednjo konfiguracijo
 * CPU: 1
 * RAM: 2GB
 * Disk: 8GB
 * NIC:
  * Gi1: Attached to Host-only Adapter
  * Gi2: Attached to Host-only Adapter
  * Gi3: Attached to Host-only Adapter
* V virtualni DVD drive vstavi ISO in instaliraj CSR usmerjevalnik
* Nastavi IP na vmesnik GigabitEthernet 1 (Ce vmesnik ne gre v stanje up, shrani konfiguracijo in restartej usmerjevalnik)
```
interface GigabitEthernet1
 ip address 192.168.35.121 255.255.255.0
 no shutdown
```
* Nastavi osnovne nastavitve:
```
aaa new-model
aaa authentication login default local
aaa authorization exec default local
username ansible privilege 15 password ansible
enable password ansible
hostname R1
ip domain name sinog.si

crypt key generate rsa modulus 2048
copy run start
```
* Preveri povezljivost med Ansible streznikom in usmerjevalnikom
```
$ ssh ansible@192.168.35.121
Password:
R1#
```
* Ugasni usmerjevalnik v VirtualBox (power off)
* Naredi clone virtualne masine (2x)
* Zazeni vse tri usmerjevalnike
* Spremeni osnovne nastavitve na drugem in tretjem usmerjevalniku
```
hostname R2
interface GigabitEthernet1
 ip address 192.168.35.122 255.255.255.0
 no shutdown
```
```
hostname R3
interface GigabitEthernet1
 ip address 192.168.35.121 255.255.255.0
 no shutdown
```
* Ponovno zazeni usmerjevalnika R2 in R3
* Preveri povezljivost do sumerjevalnikov iz Ansible streznika
```
$ ssh ansible@192.168.35.122
Password:
R2#exit
Connection to 192.168.35.122 closed by remote host.
Connection to 192.168.35.122 closed.
$ ssh ansible@192.168.35.123
Password:
R3#
R3#exit
Connection to 192.168.35.123 closed by remote host.
Connection to 192.168.35.123 closed.
```

## Posnetki virtualk
- [virtualke](https://raw.githubusercontent.com/ubajze/ansible_workshop/master/instructions/sc/screenshoot1.png)
- [ansible](https://raw.githubusercontent.com/ubajze/ansible_workshop/master/instructions/sc/screenshoot2.png)
- [CSR1000v 1](https://raw.githubusercontent.com/ubajze/ansible_workshop/master/instructions/sc/screenshoot3.png)
- [CSR1000v 2](https://raw.githubusercontent.com/ubajze/ansible_workshop/master/instructions/sc/screenshoot4.png)
- [CSR1000v 3](https://raw.githubusercontent.com/ubajze/ansible_workshop/master/instructions/sc/screenshoot5.png)

