# Windows Server - Server 1: DC
## The SQL Server Collation is incorrect after already having installed SQL!!
(The Solution)[https://www.mssqltips.com/sqlservertip/3519/changing-sql-server-collation-after-installation/]
- Change `Latin1_General_CP1_CI_AI` to `Latin1_General_CP1_CI_AS`;
- Use `MSSQLSERVER` instead of `SQLEXP2014`.