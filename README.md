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
        <li><a href="#Part-III-:-DHCP-Relay-agent-configuration">Part III : Relay agent configuration</a></li>
        <li><a href="#Part-IV">Part IV : Demonstration</a></li>
  </ol>
</details>



### Part-I

**Setup ISC DHCP server**
First we install the DHCP server.
```sh
sudo apt-get install isc-dhcp-server
```
<p align="right">(<a href="#top">back to top</a>)</p>

<!-- The PNG class -->
### Part-II

First we have to define for which network interface the ISC DHCP server should work. To do this, we open the following configuration file.
```sh
sudo nano /etc/default/isc-dhcp-server
```
Here we add the interface name in the line provided. Here we choose “wlan0” as an example for a WLAN router. Depending on the application, it can also be “eth0”.
```sh
INTERFACES = "wlan0"
```
It continues with the configuration. Before we save the default configuration file and create a new one.
```sh
sudo mv /etc/dhcp/dhcpd.conf /etc/dhcp/dhcpd.conf_old
sudo nano /etc/dhcp/dhcpd.conf
```
Then the editor opens with an empty file, in which we enter the following configuration.
```sh
authoritative;
default-lease-time 86400;
max-lease-time 86400;
 
subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.1.100 192.168.1.150;
  option routers 192.168.1.1;
  option domain-name-servers 192.168.1.1;
  option domain-name "local";
}
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


<!-- Inhertance diagram -->
### Part-III : DHCP Relay agent configuration

Un texte est une série orale ou écrite de mots perçus comme constituant un ensemble cohérent, porteur de sens et utilisant les structures propres à une langue (conjugaisons, construction et association des phrases…). ... L'étude formelle des textes s'appuie sur la linguistique, qui est l'approche scientifique du langage.


<p align="right">(<a href="#top">back to top</a>)</p>


<!-- Image -->
### Part-IV

Un texte est une série orale ou écrite de mots perçus comme constituant un ensemble cohérent, porteur de sens et utilisant les structures propres à une langue (conjugaisons, construction et association des phrases…). ... L'étude formelle des textes s'appuie sur la linguistique, qui est l'approche scientifique du langage.

<p align="right">(<a href="#top">back to top</a>)</p>

Our Team - [AIT EL KADI Ilyas](https://github.com/IlyasKadi) - [AZIZ Oussama](https://github.com/ATAMAN0)

Project Link: [Widgets_and_Layouts](https://github.com/IlyasKadi/Widgets_and_Layouts)

Encadré par : [Mr.BELCAID-Anass](https://anassbelcaid.github.io)

<p align="right">(<a href="#top">back to top</a>)</p>
