# Windows Server - Server 2: DC2
## Installation
### Perform Initial Configuration of DC2
1. Configure VM
	- **Naam:** DC2
	- **OS:** Windows Server 2016
	- **RAM:** 2 Gigabyte
	- **Virtuele Schijf:** 32 Gigabyte
	- **NIC 1:** Intern Network
		- Mark _"Cable is connected"_;
2. Install OS
	- **Operating System:** Windows Server 2016 Standard Evaluation (Desktop Experience)
		- Product Key: 6HBCC-CNBCX-XYX4T-MTYRP-XTQDF
	- **Language Settings:** English (United States)
		- Keyboard: Dutch (Belgium)
3. Configure NIC	
	- **Configure NIC**
		- Open _"Server Manager"_;
		- Click on _"Local Server"_;
		- Click on your Computer's Internal NIC;
		- Click on _"IPv4(TCP/IPv4)"_;
		- Mark _"Use the following IP address"_
			**IP Address:** 192.168.1.2
			**Subnet Mask:** 255.255.255.0
			**Default Gateway:** 192.168.1.1
		- Mark _"Use the following DNS server addresses"_:
			**Preferred DNS server:** 192.168.1.1

			**NAT CARD:** Ethernet 2

### Configure DC2 as Domain Controller
1. Rename Server:
	- Open _"Server Manager"_;
	- Click on _"Local Server"_;
	- Click on your computer's name;
	- On the _"System"_ Tab, click _"Change"_;
	- Change your computer's name;
	- reboot your device;

			**SERVER NAME:** DC2

2. Install Active Directory Domain Services
	- Open _"Server Manager"_;
	- Click on _"Add Roles and Features"_;
	- The installation
		- Click _"Next"_;
		- Select _"Role-Based Installation"_, click _"Next"_;
		- Select _"Select a server from the server pool"_, select your server, click _"Next"_;
		- Select _"Active Directory Domain Services"_;
		- A pop-up will appear, click _"Add Features"_;
		- Click _"Next"_;
		- Click _"Next"_;
		- Click _"Next"_;
		- Click _"Install"_;

3. Promote the server to DC
	- Click on the flag, click on _"Configure this server as a Domain Controller"_;
	- The installation
		- Click on _"Add a domain controller to an existing forest"_;
		- insert the Root Domain Name
			**Root Domain Name:** patwey.gent
		- remove the _"Domain Name System (DNS) Server"_ mark;
		- Insert a DSRM password:
			**DSRM:** Aa12345
		- Specify additional replication options:
			- **Replicate from:** DC1.patwey.gent
		- Click _"Next"_;
		- Click _"Next"_;
		- Click _"Next"_;
		- Click _"Install"_;

4. .NET 3.5
- Open _"Server Manager"_;
	- Click on _"Add Roles and Features"_;
	- The installation
		- Click _"Next"_;
		- Select _"Role-Based Installation"_, click _"Next"_;
		- Select _"Select a server from the server pool"_, select your server, click _"Next"_;
		- Click _"Next"_;
		- Select 