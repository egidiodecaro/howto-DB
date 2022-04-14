# CREAZIONE UTENZA SU DB Oracle
## SQL:

Istruzioni da eseguire per creare l'utenza, in questo caso denominata **academy** e con password **academy$**
		
	CREATE TABLESPACE academy_data DATAFILE '/u02/orcl/academy_data_01.dbf' SIZE 2G AUTOEXTEND ON;  

> "A database is divided into one or more logical storage units called tablespaces. Tablespaces are divided into logical units of storage called segments, which are further divided into extents. Extents are a collection of contiguous blocks."

Se la cartella non esiste, crearla manualmente. Si può usare WinSCP. Fare attenzione al "proprietario" della cartella.
Deve essere lo stesso utente che va ad eseguire le istruzioni SQL
Da qui, tutto quel che viene creato con academy finisce nel tablespace "academy_data", contenuto nel datafile "academy_data_01.dbf".
Se successivamente i 2Gb di spazio dato al file non dovessero bastare, si possono aggiungere altri datafile legati al primo.

	CREATE USER academy IDENTIFIED BY academy$ DEFAULT TABLESPACE academy_data;

Crea l'utente **academy** con passwor **academy$** , assegnandogli di default il tablespace appena definito.

	GRANT CONNECT, RESOURCE, UNLIMITED TABLESPACE TO academy;  

Serve a fornire all'utente appena creato i permessi
> The RESOURCE role grants a user the privileges necessary to create procedures, triggers and, in Oracle8, types within the user's own schema area. Granting a user RESOURCE without CONNECT, while possible, does not allow the user to log in to the database.


	GRANT CREATE VIEW TO academy; 
	GRANT CREATE MATERIALIZED VIEW TO academy;  
	GRANT CREATE SESSION TO academy;  
	GRANT CREATE SYNONYM TO academy;  
	GRANT CREATE TRIGGER TO academy;

Fornisce all'utente ulteriori permessi per la creazione di view, materialized view, session, sinonimi e trigger
	
## Reference:

* [Oracle Documentation - Tablespaces](https://docs.oracle.com/cd/B19306_01/server.102/b14220/physical.htm#i2009)
* [Oracle Documentation - User Creation](https://docs.oracle.com/cd/B19306_01/server.102/b14200/statements_8003.htm#:~:text=Use%20the%20CREATE%20USER%20statement,proxy%20application%20or%20application%20server.)
* [Oracle Documentation - GRANT](https://docs.oracle.com/javadb/10.8.3.0/ref/rrefsqljgrant.html)
* [chartio.com - How to Create a User and Grant Permissions in Oracle](https://chartio.com/resources/tutorials/how-to-create-a-user-and-grant-permissions-in-oracle/)