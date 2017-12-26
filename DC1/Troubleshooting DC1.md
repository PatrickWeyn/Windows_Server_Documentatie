# Windows Server - Server 1: DC
## I have entered the wrong Domain-name!
Since your device does not have any configurations applied to it yet, you can simply perform a clean install.
## I have configured my NICs properly, but i have no internet connection!
1. The host device's firewall could possibly block outgoing network information.
	Try the following steps for the solution
		- Open _"Windows Firewall with Advanced Security"_
		- Click _"Firewall Properties"_
		- Click on _"Customize"_ next to _"Protected Network Connections"_ in the _"Domain Profile"_ Tab;
		- Unmark each _"VirtualBox Host-Only Network"_ Adapter;
		- Apply;
2. Some networks work using different setting for your NIC.
	Try the following steps for the solution
		- EXTERNAL NIC
			- Change the NIC to "bridged" or "NAT";
		- INTERNAL NIC
			- Change the NIC to "host" or "internal";