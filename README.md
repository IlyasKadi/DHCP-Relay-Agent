<div id="top"></div>


<!-- PROJECT LOGO -->
<br />
<div align="center">
    <img src="images/logo.png" alt="Logo" width="450" height="380">
  <h2 align="center">Project 1</h2>
  <h3 align="center">Dynamic Host Configuration Protocol</h3>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
        <li><a href="#Part-I">Part I</a></li>
        <li><a href="#Part-II">Part II : DHCP configuration</a></li>
        <li><a href="#Part-III">Part III : Relay agent configuration</a></li>
        <li><a href="#Part-IV">Part IV : Demonstration</a></li>
  </ol>
</details>



### Part-I

**Setup ISC DHCP server**
First we install the DHCP server.
```sh
sudo apt-get install isc-dhcp-server
```

<!-- DHCP configuration -->
### Part-II

First we have to define for which network interface the ISC DHCP server should work. To do this, we open the following configuration file.
```sh
sudo nano /etc/default/isc-dhcp-server
```
Here we add the interface name in the line provided. Here we choose “eth1”. Depending on the application, it can also be “wlan0”.
```sh
INTERFACESv4="eth1"
INTERFACESv6=""
```
It continues with the configuration. Before we save the default configuration file and create a new one.
```sh
sudo nano /etc/dhcp/dhcpd.conf
```
Then the editor opens with an empty file, in which we enter the following configuration.
```sh
authoritative;
default-lease-time 600;
max-lease-time 7200;

subnet 192.168.1.0 netmask 255.255.255.0
{
        range 192.168.1.50 192.168.1.80;
        option routers 192.168.1.1;
        interface eth1;
}

subnet 192.168.2.0 netmask 255.255.255.0
{
        range 192.168.2.50 192.168.2.80;
        option routers 192.168.2.1;
        interface eth0;
}
```

```sh
sudo nano /etc/network/interfaces
```

```sh
auto lo
iface lo inet loopback

allow-hotplug eth0
iface eth0 inet static
        address 10.1.1.1
        gateway 10.1.1.1
        network 10.1.1.0
        netmask 255.255.255.0

allow-hotplug eth1
iface eth1 inet static
        address 192.168.1.1
        gateway 192.168.1.1
```

Then the DHCP server has to be started.
```sh
sudo systemctl start isc-dhcp-server
```
If the command prompt returns without a message, then it worked.

If the start of the ISC DHCP server was aborted with an error, then you should perform a status query to get to the bottom of the error.
```sh
sudo systemctl status isc-dhcp-server
```
In case of error, the messages are unfortunately not always clear. Unless you have made a configuration error. Very popular are typos or missing semicolons (“;”) at the end of a directive.

<p align="right">(<a href="#top">back to top</a>)</p>


<!-- Relay agent configuration -->
### Part-III

**Setup ISC DHCP RELAY**
First we install the DHCP relay agent.
```sh
apt install isc-dhcp-relay
```
First we have to define for which network interface the ISC DHCP server should work. To do this, we open the following configuration file.
```sh
sudo nano /etc/default/isc-dhcp-relay
```
Here we add the ADDRESS of dhcp and interfaces names.
```sh
# What servers should the DHCP relay forward requests to?
SERVERS="10.1.1.1"

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES="eth0 eth1"

# Additional options that are passed to the DHCP relay daemon?
OPTIONS=""
```

```sh
sudo nano /etc/network/interfaces
```

```sh
auto lo
iface lo inet loopback

allow-hotplug eth1
iface eth1 inet static
        address 10.1.1.2
        gateway 10.1.1.2
        network 10.1.1.0
        netmask 255.255.255.0

allow-hotplug eth0
iface eth0 inet static
        address 192.168.2.1
        gateway 192.168.2.1
        network 192.168.2.0
        netmask 255.255.255.0

```
Then the DHCP relay has to be started.
```sh
sudo systemctl start isc-dhcp-relay
```
If the command prompt returns without a message, then it worked.

If the start of the ISC DHCP relay was aborted with an error, then you should perform a status query to get to the bottom of the error.
```sh
sudo systemctl status isc-dhcp-relay
```


<p align="right">(<a href="#top">back to top</a>)</p>


<!-- Demonstration -->
### Part-IV

Un texte est une série orale ou écrite de mots perçus comme constituant un ensemble cohérent, porteur de sens et utilisant les structures propres à une langue (conjugaisons, construction et association des phrases…). ... L'étude formelle des textes s'appuie sur la linguistique, qui est l'approche scientifique du langage.

<p align="right">(<a href="#top">back to top</a>)</p>

Our Team - [AIT EL KADI Ilyas](https://github.com/IlyasKadi) - [AZIZ Oussama](https://github.com/ATAMAN0)

Project Link: [Widgets_and_Layouts](https://github.com/IlyasKadi/Widgets_and_Layouts)

Encadré par : [Mr.BELCAID-Anass](https://anassbelcaid.github.io)

<p align="right">(<a href="#top">back to top</a>)</p>
