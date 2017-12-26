# Windows Server - ExchangeSQL
## Installation
### Perform Initial Configuration of ExchangeSQL
1. Configure VM
	- **Naam:** ExchangeSQL
	- **OS:** Windows Server 2012 R2
	- **RAM:** 2 Gigabyte
	- **Virtuele Schijf:** 90 gigabyte
	- **NIC:** Intern Network
		- Name: Intnet
		- Mark _"Cable is connected"_;
2. Install OS
	- **Operating System:** Windows Server 2012 R2
		- Product Key: QTMYN-8CRFY-CYB79-TFXQP-4RFRY
	- **Language Settings:** English (United States)
		- Keyboard: Dutch (Belgium)
3. Configure NIC
	- **Configure NIC**
		- Open _"Server Manager"_;
		- Click on _"Local Server"_;
		- Click on your Computer's Internal NIC;
		- Click on _"IPv4(TCP/IPv4)"_;
		- Mark _"Use the following IP address"_
			**IP Address:** 192.168.1.3
			**Subnet Mask:** 255.255.255.0
			**Default Gateway:** 192.168.1.1
		- Mark _"Use the following DNS server addresses"_:
			**Preferred DNS server:** 192.168.1.1

			**NAT CARD:** Ethernet

4. Configure name & domain
	- Open _"Server Manager"_;
	- Click on _"Local Server"_;
	- Click on your computer's name;
	- On the _"System"_ Tab, click _"Change"_;
	- Change your computer's name;

		**Computer Name:** Exsql

	- Click on _"Domain"_;
	- Change your domain name;

		**Domain:** patwey.gent

	- reboot your device;
  	
5. Install .Net 3.5

6. Install GuestAdditions

### Install SQL
  - Start the _SQL Server 2012_ installation;
  - Click on _Installation_;
  - Click on _New SQL Server stand alone Installation..._;
  - Click _Next_;
  - If the _Setup Support Rules_ Generates a warning, follow this subsection;

  	- Open windows firewall;
  		- Open _Run_;
  		- type _WF.msc_;
  	- Right-click on _Inbound Rules, select _New Rule_;
  	- Select _Program_;
  	- Click _Next_;
  	- Write down _C:\Program Files\Microsoft SQL Server\MSSQL13.SQLEXPRESS\MSSQL\Binn\SQLServr.exe_;
  	- Click _Next_;
  	- Click _Next_;
  	- Click _Next_;
  	- Fill in the name _SQLServer_;
  	- Click _Next_;
  	
  - Click _Next_;
  - Mark _I accept the license terms_;
  - Click _Next_;
  - Click _Next_;
  - Click _Select All_;
  - Click _Next_;
  - Click _Next_;
  - Click _Next_;
  - Click _Next_;
  - Change the owner of the services _SQL Server Agent_ and _SQL Server Database Engine_;
  	- Click on _NT Service/..._;
  	- Select _Browse_ in the drop-down list;
  	- Click _Advanced_;
  	- Log in with the domain's admin credentials;
  	- Click _Find Now_;
  	- Select _System_ in the search results;
  	- Click _OK_;
  	- Click _OK_;
  - Change the Startup Type of the _SQL Server Agent_ to _Automatic_;
  - Click _Next_;
  - Click _Add Current User_;
  - Remove all other Users;
  - Click _Next_;
  - Click _Add Current User_;
  - Click _Next_;
  - Click _Next_;
  - Click _Next_;
  - Click _Next_;
  - Click _Next_;
  - Click _Next_;
  - Click _Next_;
  - Click _Install_;
  - Click _Close_;
  - Restart server;
  - Open _SQL Server Config Manager_;
  - Select _SQL Server Services_;
  - Right-click _SQL Server_;
  - Click _Properties_;
  - Select _FILESTREAM_;
  - Mark all options;
  - Click _OK_;