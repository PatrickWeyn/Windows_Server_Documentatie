# Windows Server - ExchangeSQL
## Installation
### Perform Initial Configuration of ExchangeSQL
1. Follow the steps in the document _[Installatie SQL.md](Installatie_SQL.md)_;
2. After reaching the end of the document, perform the following steps;
3. Perform _Windows Update_;
4. Run the following Commands in _Powershell_:
	- Install-WindowsFeature RSAT-ADDS
	- Install-WindowsFeature AS-HTTP-Activation, Desktop-Experience, NET-Framework-45-Features, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-Mgmt, RSAT-Clustering-PowerShell, Web-Mgmt-Console, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, Windows-Identity-Foundation
5. Install _Media Foundation_
	- Open _Server Manager_;
	- Run the _Open Roles and Services Wizard_;
	- Under features, select _Media Foundation_;
	- Finish the installation;
5. Install _Microsoft Unified Communications Managed API 4.0_
	- Accept the _License Terms_;
	- Install and Finish;

### Install Exchange
  - Don't check for updates;
  - Wait for the files to be copied, and the resources to be loaded;
  - Accept the terms in the license agreement;
  - Do not use the recommended settings;
  - Select the Mailbox role, and automatically install Windows Server Role Features;
  - Keep the default Path;
  - Rename the Exchange Organizations;

  	**Exchange name:** patwey

  - Do not disable malware scanning;
  - Wait for the readiness checks to be completed;
  - Install;
  -Restart

### Configure Exchange
  - Open _https://exsql/owa/auth/logon.aspx?replaceCurrent=1&url=https%3a%2f%2fexsql%2fecp%2f%3fExchClientVer%3d15_;
  - Log in with administrator credentials;
  
  1. Configure User Mailbox
 	- Click on _geadresseerden_;
 	- Click on _postvakken_;
 	- Click on _add_ and select _user mailbox_;
 	- Add the users:
 		- **Voornaam:** Diana	/ Denis		/ Daniel	/ Craig		/ Beth
 		- **Achternaam:** Walda	/ Mathers	/ James		/ Watcher	/ Raw
 		- **Aanmeldingsnaam:** dia.wal / den.mat / dan.jam / cra.wat / bet.raw
 		- **Wachtwoord:** Aa12345

  2. Configure Send and Receive Emails
    - Click on _e-mailstroom_;
    - Select _connectors verzenden_;
    - Click on _add_;
    - Add the Name:
    	- **Naam:** Send Connector
    - Select _Internet_;
    - Click _Next_;
    - Select _MX-record..._
    - Click _Next_;
    - Click _Add_;
    - Add the FQDN:
    	- **FQDN:** *
    - Click _Next_;
    - Click _Add_;
    - Select your SQL Server;
    - Click _Finish_;

  3. Configure External and Internal URLs
    - Click on _servers_;
    - Click on _virtual directories_;
    **OWA**
    - Double-click on _owa_;
    - Change internal and external URL;
      _**Internal and External URL:**_ https://exsql.patwey.gent/owa
    **ECP**
    - Double-click on _ecp_;
    - Change internal and external URL;
      _**Internal and External URL:**_ https://exsql.patwey.gent/ecp
    **Activesync**
    - Double-click on _Microsoft-Server-ActiveSync_;
    - Change internal and external URL;
      _**Internal and External URL:**_ https://exsql.patwey.gent/Microsoft-Server-ActiveSync
    **OAB**
    - Double-click on _OAB_;
    - Change internal and external URL;
      _**Internal and External URL:**_ https://exsql.patwey.gent/OAB
    **EWS**
    - Double-click on _EWS_;
    - Change internal and external URL;
      _**Internal and External URL:**_ https://exsql.patwey.gent/EWS/Exchange.asmx
    **Outlook anywhere**
    - Click on _servers_;
    - Double-click the server;
    - Select _Outlook Anywhere_;
    - Change internal and external URL;
      _**Internal and External URL:**_ exsql.patwey.gent
    **Auto Discover**
    - Open _Exchange Management Shell_;
    - Run the following command:
      _**Command:**_ Set-ClientAccessServer -Identity exsql -AutoDiscoverServiceInternalUri https://autodiscover.patwey.gent/Autodiscover/Autodiscover.xml
      **FAILED**
        - object 'MBG-MAIL' couldn't be found on 'DC1.patwey.gent'.

  5. Configure URL directions
    - Open _IIS Manager_;
      - Open _Server Manager_;
      - Click _Tools_;
      - Click _IIS_;
    - Click on the arrow next to your server;
      - There could be a pop-up, click No;
    - Click on the arrow next to _Sites_;
    - Click on _Default Web Site_;
    - Double-click _SSL settings_;
    - Uncheck _Require SSL_;
    - Click _Apply_;
    - Double-click _HTTP Redirect_;
    - Mark _Redirect requests to this destination:_;
    - Fill in the new URL:
      _**Redirection URL**_: https://mail.patwey.be/owa
    - Mark _Only redirect requests to content in this diretory (not subdirectories);
    - Click _Apply_;
    - Uncheck the _HTTP Redirect Option_ from all subdirectories;
    - Select _ecp_;
    - Double-click _SSL-Settings_;
    - Mark _Require SSL_;
    - Click _Apply_;
    - Restart iis;
      _**Command:**_ iisreset /noforce

  _Now repeat this process for **Exchange Back End** instead of **Default Web Site**_