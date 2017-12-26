# Windows Server - Server 1: DC
## Domeincontroller
  1. Gebruikers moeten van overal kunnen inloggen met een account gemaakt in DC1;
	- Log in op DC1 met de gebruiker
		**Gebruikersnaam:** administrator
		**Wachtwoord:** Aa123
	- Open _Server Manager_;
	- Klik op _Tools_, en selecteer _Active Directory Users and Computers_;
	- Navigeer door _patwey.gent_ naar de _Users_ folder;
	- Klik op _Create a new User in the current container_;
	- Creer een willekeurige gebruiker;
	- Laat DC 1 aanstaan;

	- Log in op een extern toestel met de nieuw aangemaakte gebruiker;

	**Mogelijke Fouten**
	1. De gebruiker vindt de Tool _Active Directory Users and Computers_ niet;
		**Oorzaak**
			AD DS is niet geinstalleerd
		**Oplossing**
			Installeer AD DS
	2. De gebruiker vindt het domein _patwey.gent_ niet;
		**Oorzaak**
			het domein staat verkeerd ingesteld;
		**Oplossing**
			Spijtig genoeg kan men enkel een clean install doen;
	3. De gebruiker kan niet inloggen op een intern toestel met de nieuwe aangemaakte gebruiker;
		**Oorzaak 1**
			DC 1 staat niet aan;
		**Oplossing 1**
			Zet DC 1 aan;

		**Oorzaak 2**
			Het intern toestel zit niet in het domein;
		**Oplossing 2**
			Steek het intern toestel in het domein;
		
		**Oorzaak 3**
			Een netwerkkaart staat verkeerd ingesteld;
		**Oplossing 3**	
			Overloop de configuratie van de netwerkkaarten verantwoordelijk voor het intern netwerk van zowel DC 1 alsook het intern toestel

		**Oorzaak 4**
			De netwerkkaarten hebben de verkeerde instelling in Virtualbox;
		**Oplossing 4**
			Probeer de combinaties:
				1. Intern-Intern
				2. Host-Host

## Routering