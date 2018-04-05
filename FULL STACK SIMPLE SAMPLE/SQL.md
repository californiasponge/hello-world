##FULL STACK EXAMPLE

**SQL STORED PROCEDURE CREATE NEW USER**  
ALTER PROC [dbo].[users_insert]  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@id INT OUTPUT,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@first_name NVARCHAR(150),   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@last_name NVARCHAR(150),  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@age INT,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@weight INT,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@height INT,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@email NVARCHAR(150),  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@password NVARCHAR(255)  

AS

INSERT INTO Users  
&nbsp;&nbsp;(first_name, last_name, age, weight, height, email, password)

VALUES  
&nbsp;&nbsp;(@first_name, @last_name, @age, @weight, @height, @email, @password)

SET  
&nbsp;&nbsp;@id = SCOPE_IDENTITY()

/* ----------------------------------------------------------TEST BLOCK-------------------------------------------------------------  

	DECLARE	@id INT,  
		@first_name NVARCHAR(150),   
		@last_name NVARCHAR(150),  
		@age INT,  
		@weight INT,  
		@height INT,  
		@email NVARCHAR(150),  
		@password NVARCHAR(255)  
		
	EXECUTE Users_Insert @id, @first_name, @last_name, @age, @weight, @height, @email, @password

	SELECT first_name, last_name, age, weight, height, email, password, date_created, date_modified
	FROM Users
-----------------------------------------------------------------------------------------------------------------------------------*/
