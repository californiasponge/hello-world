## STORED PROCEDURES: 

**BELOW ARE 5 EXAMPLE SP's - INSERT, UPDATE, DELETE, GET BY ID, LOGIN**

**CREATE NEW USER**  
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

****************************************************************************************************************

**LOG IN USER**  
ALTER PROC [dbo].[users_login]  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@user_login nvarchar(255)  

AS

SELECT id, password, email  

FROM Users  

WHERE @user_login = email  


/* ----------------------------------------------------------TEST BLOCK-------------------------------------------------------------  

	EXECUTE users_login  
		@user_login = 'testEmail@gmail.com'  

-----------------------------------------------------------------------------------------------------------------------------------*/

****************************************************************************************************************

**GET ALL NOTIFICATIONS BY USER**  
ALTER PROC [dbo].[Notifications_getAllByUser]  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@id INT  

AS

SELECT * FROM Notifications  
	 JOIN Notification_RecipientIds ON notification_id = id  
	 WHERE student_user_id = @id  

/* ----------------------------------------------------------TEST BLOCK-------------------------------------------------------------  

	EXECUTE Notifications_getAllByUser 3  

-----------------------------------------------------------------------------------------------------------------------------------*/

****************************************************************************************************************

**DELETE A BLOG POST**  
ALTER PROC [dbo].[Blogs_delete]   
		@id int

AS 

DELETE FROM Blogs  
WHERE id = @id

IF @@rowcount = 0  
throw 51000,'Cannot delete because that post does not exist', 1


/* ----------------------------------------------------------TEST BLOCK-------------------------------------------------------------  

	DECLARE @id int = 10000

	EXECUTE Blogs_delete @id

-----------------------------------------------------------------------------------------------------------------------------------*/

****************************************************************************************************************

**UPDATE USER**  
ALTER PROC [dbo].[users_update]  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@id INT,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@first_name NVARCHAR(150),  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@last_name NVARCHAR(150),  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@age INT,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@weight INT,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@height INT,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@email NVARCHAR(150),  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@password NVARCHAR(255)  

AS

UPDATE Users

SET&nbsp;&nbsp;&nbsp;&nbsp;first_name = @first_name,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;last_name = @last_name,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;age = @age,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;weight = @weight,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;height = @height,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;email = @email,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;password = @password,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;date_modified = GETUTCDATE()  

WHERE id = @id

/* ----------------------------------------------------------TEST BLOCK------------------------------------------------------------- 

	DECLARE @id INT,  
		@first_name NVARCHAR(150),  
		@last_name NVARCHAR(150),  
		@age INT,  
		@weight INT,  
		@height INT,  
		@email NVARCHAR(150),  
		@password NVARCHAR(255)  
		
	EXECUTE users_update @first_name, @last_name, @age, @weight, @height, @email, @password  
	
	SELECT first_name, last_name, age, weight, height, email, password, date_created, date_modified
	FROM Users
-----------------------------------------------------------------------------------------------------------------------------------*/
