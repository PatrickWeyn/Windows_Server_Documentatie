# Windows Server - Server 1: DC
## The SQL Server Collation is incorrect after already having installed SQL!!
- Change `Latin1_General_CP1_CI_AI` to `Latin1_General_CP1_CI_AS`;
- Use `MSSQLSERVER` instead of `SQLEXP2014`.