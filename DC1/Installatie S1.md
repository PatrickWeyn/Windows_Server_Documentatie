# Windows Server - Server 1: DC
## Installation
### Perform Initial Configuration of DC1
1. Configure VM
	- **Naam:** DC1
	- **OS:** Windows Server 2016
	- **RAM:** 2 Gigabyte
	- **Virtuele Schijf:** 20 Gigabyte
	- **NIC 1:** Bridged/NAT
		- Mark `Cable is connected`;
	- **NIC 2:** Intern Network
		- Name: Intnet
		- Mark `Cable is connected`;
2. Install OS
	- **Operating System:** Windows Server 2016 Standard Evaluation (Desktop Experience)
		- Product Key: 6HBCC-CNBCX-XYX4T-MTYRP-XTQDF
	- **Language Settings:** English (United States)
		- Keyboard: Dutch (Belgium)
3. Configure NIC
	- **Configure NIC 1**
		- Open `Server Manager`;
		- Click on `Local Server`;
		- Click on your Computer's External NIC;
		- Click on `IPv4(TCP/IPv4)`;
		- Mark `Obtain an IP address automatically`;
			
			**NAT CARD:** Ethernet
	
	- **Configure NIC 2**
		- Open `Server Manager`;
		- Click on `Local Server`;
		- Click on your Computer's Internal NIC;
		- Click on `IPv4(TCP/IPv4)`;
		- Mark `Use the following IP address`
			**IP Address:** 192.168.1.1
			**Subnet Mask:** 255.255.255.0
			**Default Gateway:** empty
		- Mark `Use the following DNS server addresses`:
			**Preferred DNS server:** 192.168.1.1

			**NAT CARD:** Ethernet 2

### Configure DC1 as Domain Controller
1. Rename Server:
	- Open `Server Manager`;
	- Click on `Local Server`;
	- Click on your computer's name;
	- On the `System` Tab, click `Change`;
	- Change your computer's name;
	- reboot your device;

			**SERVER NAME:** DC1

2. Install Active Directory Domain Services
	- Open `Server Manager`;
	- Click on `Add Roles and Features`;
	- The installation
		- Click `Next`;
		- Select `Role-Based Installation`, click `Next`;
		- Select `Select a server from the server pool`, select your server, click `Next`;
		- Select `Active Directory Domain Services`;
		- A pop-up will appear, click `Next`;
		- Mark `Net Framework 3.5 Features`;
		- Click `Next`;
		- Click `Install`;

3. Promote the server to DC
	- Click on the flag, click on `Configure this server as a Domain Controller`;
	- The installation
		- Click on `Add a new Forest`;
		- Insert the Root Domain Name;
			**Root Domain Name:** patwey.gent

		- Select the Forest Functional Level and the Domain Functional Level;
			**FFL:** Windows Server 2012 R2
			**DFL:** Windows Server 2012 R2

		- insert a DSRM;
			**DSRM:** Aa123
			
		- click `Next`;
		- Click `Next`;
		- Click `Next`;
		- Click `Next`;

### Configure DC1 as Router
1. Install Routing and Remote Access
	- Click on `Add Roles and Features`;
	- The installation
		- Click `Next`;
		- Select `Role-Based Installation`, click `Next`;
		- Select `Select a server from the server pool`, select your server, click `Next`;
		- Select `Remote Access`;
		- Click `Next`;
		- Click `Next`;
		- Click `Next`;
		- Select `Routing`;
		- A pop-up will appear, click `Add Features`;
		- Click `Next`;
		- Click `Next`;
		- Click `Next`;
		- Click `Install`;
		- Wait for the installation to finish;
		- Click `Close`;
2. Configuring Routing and Remote Access
	- Click on `Tools`;
	- Click on `Routing and Remote Access`;
	- Right-click on `DC1(local)`;
	- Click on `Configure and Enable Routing and Remote Access`;
	- Click `Next`;
	- Select `Custom Configuration`;
	- Click `Next`;
	- Select `NAT` and `LAN routing`;
	- Click `Next`;
	- Click `Finish`;
	- A pop-up will appear, click `Start Service`;
	- After the Service has started, click on `IPv4`;
	- Right-click on `NAT`;
	- Select `New Interface`;
	- **NIC 1**
		- Select your NAT interface;
		- Click `OK`;
		- Select _Public interface connected to the Internet_;
		- Mark _Enable NAT on this interface_;
		- Click _Apply_ and _OK_;
	- **NIC 2**
		- Select your intern interface;
		- Click _OK_;
		- Select _Private interface connected to private network_;
		- Click _OK_;

### Configure DC1 as DHCP server
1. Install DHCP server
	- Open `Server Manager`;
	- Click on `Add Roles and Features`;
	- The installation
		- Click `Next`;
		- Select `Role-Based Installation`, click `Next`;
		- Select `Select a server from the server pool`, select your server, click `Next`;
		- Select `DHCP Features`;
		- A pop-up will appear, click `Add Features`;
		- Click `Next`;
		- Click `Next`;
		- Click `Install`;
		- Click `Close`;
	- Click the flag;
	- Select `Complete DHCP Configuration`;
	- Click `Next`;
	- Click `Commit`;
	- Click `Close`;
2. Configure DHCP
	- Open `Server Manager`;
	- Click on `Tools`;
	- Click `DHCP`;
	- Expand `DC1.patwey.gent`;
	- Right-click `IPv4`;
	- Select `New Scope`;
	- Click `Next`;
	- Give the DHCP-scope a name

		**NAME:** DHCP-Clients

	- Click `Next`;
	- Configure the Scope as follows:

		**START:** 192.168.1.100
		**END:** 192.168.1.200
		**LENGTH:** 24
		**SUBNET:** 255.255.255.0

	- Click `Next`;
	- Click `Next`;
	- Change `Days` to 1;
	- Click `Next`;
	- Click `Next`;
	- Add the IP-address `192.168.1.1`;
	- Click `Next`;
	- Add the IP-address `192.168.1.1` & `192.168.1.2`;
	- Remove all others;
	- Click `Next`;
	- Click `Next`;
	- Click `Next`;
	- Click `Finish`;

### Preparing DC1 for SCCM
1. Configuring ADSI-edit for SCCM (Add SCCM to domain first!)
	1. Part one
		- Open `Server Manager`;
		- Click on `Tools`;
		- Click on `ADSI Edit`;
		- Right-click on `ADSI Edit`, and select `Connect To...`;
		- Do not change anything in `Connection Settings`, click `OK`;
		- Expand the newly created `Default Naming Context` and `DC=patwey,DC=gent`, right-click `CN=System`, Hover over `New`, and select `Object`;
		- Select the class as `container`, and click `Next`;
		- Provide the value as `System Management`, and click `Next`;
		- Click `Finish`;
	2. Part two
		- Open `Server Manager`;
		- Click on `Tools`;
		- Click on `Active Directory Users and Computers`;
		- Click on `View`;
		- Click on `Advanced Features`;
		- Expand `patwey.gent -> System`;
		- Right click on `System Management`;
		- Select `Delegate Control`
		- A screen pops up, click `Next`;
		- Select `Add...`
		- Click on `Object Types`;
		- Mark `Computers`, press `OK`;
		- Add `SCCM`;
		- Click `Next`;
		- Select `Create a custom task to delegate`
		- Click  `Next`;
		- Select `This folder, existing objects...`
		- Click `Next`;
		- Mark all options;
		- Click `Next`;
		- Click `Finish`;
2. Configuring Firewall GPOS
	- Open `Group Policy Management`;
	- Right click the domain, select `Create a GPO...`
	- Fill in a name for the GPO:

		**GPO NAME:** Client Push

	- Click `OK`;
	- Right-click `Client Push`;
	- Click `Edit`;
	- Under `Computer Configuration`, open `Policies`, `Windows Settings`, `Security Settings`, `Windows Firewall with Advanced security`;
	- Right click on `Inbound Rules` (repeat for `Outbound Rules`);
		- Click `New Rule...`;
		- Click `Predefined`, select `File and Printer Sharing`;
		- Click `Next`;
		- Click `Allow the connection`;
		- Click `Finish`;
	- Right click on `Inbound Rules`;
		- Click `New Rule...`;
		- Click `Predefined`, select `WMI`;
		- Click `Next`;
		- Click `Allow the connection`;
		- Click `Finish`;
	- Right click the domain, select `Create a GPO...`
	- Fill in a name for the GPO:

		**GPO NAME:** SQL

	- Click `OK`;
	- Right-click `SQL`;
	- Click `Edit`;
	- Under `Computer Configuration`, open `Policies`, `Windows Settings`, `Security Settings`, `Windows Firewall with Advanced security`;
	- Right click on `Inbound Rules` (repeat for PORT 4022);
		- Click `New Rule...`;
		- Click `PORT`;
		- Click `Next`;
		- Click `TCP` and `Specific Local Ports:` 1433;
		- Click `Next`;
		- Click `Allow the connection`;
		- Click `Next`;
		- Click `Next`;
		- Give in the name `1433 IN`;
		- Click `Finish`;
	-run `gpudate /force` in CMD;