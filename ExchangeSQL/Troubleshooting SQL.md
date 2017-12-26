# Windows Server - Server 3: SQL
  - Installing .NET 3.5 returns an error:
		Installation of one or more roles, role services, or features failed.
		The source files could not be found. Try installing the roles, role services, or features again in a new Add Roles and Features Wizard session, and on the Confirmation page of the wizard, click "Specify an alternate source path" to specify a valid location of the source files that are required for the installation. The location must be accessible by the computer account of the destination server.
	**SOLUTION:**
		- Insert the installation DVD;
		- Start the ADD ROLES AND FEATURES Wizard and click the obvious choices up until the CONFIRMATION screen;
		- On the CONFIRMATION screen of the ADD ROLES AND FEATURES WIZARD, you need to click the SPECIFY SOURCE link (tiny link at the bottom of the window);
		- Point the source path to D:\sources\sxs\ (obviously change D:\ to whatever your DVD drive letter is).