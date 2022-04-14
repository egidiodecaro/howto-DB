# CREAZIONE UTENZA SU DB Oracle
## SQL:

Istruzioni da eseguire per creare l'utenza, in questo caso denominata **academy** e con password **academy$**
		
	CREATE TABLESPACE academy_data DATAFILE '/u02/orcl/academy_data_01.dbf' SIZE 2G AUTOEXTEND ON;  
	CREATE USER academy IDENTIFIED BY academy$ DEFAULT TABLESPACE academy_data;  
	GRANT CONNECT, RESOURCE, UNLIMITED TABLESPACE TO academy;  
	GRANT CREATE VIEW TO academy;  
	GRANT CREATE MATERIALIZED VIEW TO academy;  
	GRANT CREATE SESSION TO academy;  
	GRANT CREATE SYNONYM TO academy;  
	GRANT CREATE TRIGGER TO academy;
