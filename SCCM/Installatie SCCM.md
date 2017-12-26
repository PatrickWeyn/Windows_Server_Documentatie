# Windows Server - SCCM
## Installation
### Perform Initial Configuration of SCCM
1. Configure VM
	- **Naam:** SCCM
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
			**IP Address:** 192.168.1.5
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

		**Computer Name:** SCCM

	- Click on _"Domain"_;
	- Change your domain name;

		**Domain:** patwey.gent

	- reboot your device;

5. Install .Net 3.5

6. Install GuestAdditions

7. Extend AD Schema (After SCCM prerequisites on DC1)
	- Insert the SCCM install disc;
	- Navigate to `\SMSSETUP\BIN\X64`
	- shift+right-click on `extadsch.exe`;
	- Select `Copy as Path`;
	- Open CMD;
	- Paste and run;

## Prerequisites for SCCM 2012 R2
1. Roles and Features
	- Click on `Server Manager`;
	- Click on `Add Roles and Features`;
	- Click `Next`;
	- Click `Next`;
	- Click `Next`;
	- Select `Web Server (IIS)`;
	- Click `Add Features`;
	- Click `Next`;
	- Select `.Net Framework 3.5 Features [Install all sub features], .Net Framework 4.5 Features [Install all sub features], BITS, Remote Differential Compression`;
	- Click `Next`;
	- Click `Next`;
	- Select: 
		- `Common HTTP Features – Default Document, Static Content.`
		- `Application Development – ASP.NET 3.5, .NET Extensibility 3.5, ASP.NET 4.5, .NET
		Extensibility 4.5, ISAPI extensions.`
		- `Security – Windows Authentication.`
		- `IIS 6 Management Compatibility – IIS Management Console, IIS 6 Metabase
		Compatibility, IIS 6 WMI Compatibility, IIS Management Scripts and Tools.`
	- Click `Next`;
	- Install;
2. ADK
	- right-click `adksetup.exe`;
	- select `Run as Administrator`;
	- Click `Next`;
	- Click `Next`;
	- Click `Accept`;
	- Select `Deployment Tools, Windows PE, USMT`;
	- Click `Install`;
3. SQL Server 2012 SP1 (voor download link: Zie exsql)
	- Insert the Disk;
	- right-click `setup.exe`;
	- Select `Run as administrator`;
	- Click `Installation`;
	- Click `New SQL Server stand-alone...`;
	- Click `OK`;
	- Click `OK`;
	- Click `Next`;
	- Select `I accept the license terms`;
	- Click `Next`;
	- Click `Next`;
	- Click `Next`;
	- Click `Next`;
	- Select `Database Engine Services, Reporting Services - Native, Management Tools - Complete`;
	- Click `Next`;
	- Click `Next`;
	- Click `Next`;
	- Click `Next`;
	- Select `Automatic, PATWEY\administrator, Aa123` for all services except `SQL server browser`;
	- Click `Next`;
	- Select `Add Current User`;
	- Click `Next`;
	- Click `Next`;
	- Click `Next`;
	- Click `Next`;
	- Click `Install`;
	- Click `Close`;
	- Open `SQL Server Management Studio`;
	- Log in;
	- right click `SCCM`;
	- Click `Properties`;
	- Click `Memory`;
	- Set `Minimum & Maximum` to 8192MB;
	- Click `OK`;
4. WSUS
	- Open `Server Manager`;
	- Click `Add roles and features`;
	- Click `Next`;
	- Click `Next`;
	- Click `Next`;
	- Click `Windows Server Update Services`;
	- Click `Add Features`;
	- Click `Next`;
	- Click `Next`;
	- Click `Next`;
	- Select `Database`, de-select `WID Database`;
	- Click `Next`;
	- Add a folder to which WSUS will write its stuff;

		**Location:** C:\WSUS

	- Click `Next`;
	- Insert your Database server

		**Server:** SCCM.PATWEY.GENT

	- Click `Next`;
	- Click `Install`;
	- Click `Close`;

## Install SCCM
1. Prepare the install location for SCCM
	- Create a folder and put the ISO file there;

		**LOCATION:** C:\SCCM

2. Configure SQL Collation
	- Open CMD;
		- run `NET STOP "SQL SERVER (MSSQLSERVER)"`;
		- navigate to `Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn`
		- run `sqlservr -m -T4022 -T3659 -s"MSSQLSERVER" -q"SQL_Latin1_General_CP1_CI_AS"`;
		- run `NET START "SQL SERVER (MSSQLSERVER)"`;

3. Install SCCM
	- Run the ISO file;
	- Run `splash`;
	- Click `Install`;
	- Click `Next`;
	- Click `Next`;
	- Click `Install the evaluation edition`;
	- Click `Next`;
	- Click `I accept these license terms`;
	- Click `Next`;
	- Click `I accept these license terms` for all three subjects;
	- Click `Next`;
	- Click `Download required files` and download the files to a location;
	- Click `Next`;
	- Click `Next`;
	- Fill in:

		**Site Code:** IND
		**Site Name:** SCCM VM

	- Click `Next`;
	- Click `Install the primary site as a stand-alone site`;
	- Click `Next`;
	- Click `Yes`;
	- Click `Next`;
	- Click `Next`;
	- Click `Next`;
	- Click `Configure the communication...`;
	- Click `Next`;
	- Click `Next`;
	- Click `I don't want to join...`;
	- Click `Next`;
	- Click `Begin Install`;
