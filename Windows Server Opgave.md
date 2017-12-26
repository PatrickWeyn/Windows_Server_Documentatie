# Windows Server
## Opdracht
U bent IT-consultant en krijgt de vraag om een voorstel te maken en te demonstreren van een Windowsomgeving.

De Client wenst een redundante oplossing voor zijn servers. Dit vooral op de domeincontrllers De client wenst ook dat er een mailomgeving geïnstalleerd iwordt en een omgeving die toelaat om op een efficiënte manier Windows toestellen te installeren en adopteren.

## De situatie
  - **Specificaties**
  	- Domeinnaam: patwey.gent
  - **Opdrachten**
  	- Stuur een mail naar dirk.thijs@pcprof.be;
  	- Een windows client installeren via een image;
  	- Adobe Reader installeren;
  	- Updates beheren;
  	- Documentatie;
  		1. Stappenplan
  		2. Testplan
  		3. Automatisatie
  		4. Troubleshooting
  - **Domeincontroller 1 / Router**
  	- OS: Windows Server 2016
  	- IP
  		- NIC 1: NAT
  		- NIC 2: Intern netwerk
  			IP: 192.168.1.1
  			SN: 255.255.255.0
  	- Testplan (opt.)
  	- Stappenplan (opt.)
  	- Automatisatie (opt.)
  	- Troubleshooting (opt.)
  - **Domeincontroller 2**
  	- OS: Windows Server 2016
  	- IP
  		- NIC 1: Intern netwerk
  			IP: 192.168.1.2
  			SN: 255.255.255.0
  			DG: 192.168.1.1
  	-Testplan (opt.)
  	-Stappenplan (opt.)
  	-Automatisatie (opt.)
  	- Troubleshooting (opt.)
  - **SQL server / Exchange server**
  	- OS: Windows Server 2016
  	- Exchange: Exchange Server 2016 CU3
  	- SQL: SQL server 2016
  	- IP
  		- NIC 1: Intern netwerk
  			IP: 192.168.1.3
  			SN: 255.255.255.0
  			DG: 192.168.1.1
  	-Testplan (opt.)
  	-Stappenplan (opt.)
  	-Automatisatie (opt.)
  	- Troubleshooting (opt.)
  - **Deployment server**
  	- OS: Windows Server 2012
  	- SCCM: SCCM 2012
  	- IP
  		- NIC 1: Intern netwerk
  			IP: 192.168.1.5
  			SN: 255.255.255.0
  			DG: 192.168.1.1
  	-Testplan (opt.)
  	-Stappenplan (opt.)
  	-Automatisatie (opt.)
  	- Troubleshooting (opt.)
  - **Windows Client**
  	- OS: Windows 10
  	- IP: DHCP
  	- Office software om te mailen
