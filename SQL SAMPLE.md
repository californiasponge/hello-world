## STORED PROCEDURES:

###**CREATE NEW USER**
ALTER PROC [dbo].[users_insert]
		@id INT OUTPUT,
		@first_name NVARCHAR(150),
		@last_name NVARCHAR(150),
		@age INT,
		@weight INT,
		@height INT,
		@email NVARCHAR(150),
		@password NVARCHAR(255)

AS

INSERT INTO Users
(first_name, last_name, age, weight, height, email, password)

VALUES
(@first_name, @last_name, @age, @weight, @height, @email, @password)

SET
@id = SCOPE_IDENTITY()

/* ------------------------------TEST BLOCK-----------------------------------
	DECLARE	@id INT,
		@first_name NVARCHAR(150),
		@last_name NVARCHAR(150),
		@age INT,
		@weight INT,
		@height INT,
		@email NVARCHAR(150),
		@password NVARCHAR(255) 
		
	EXECUTE Users_Insert
			@id, @first_name, @last_name, @age, @weight, @height, @email, @password

	SELECT first_name, last_name, age, weight, height, email, password, date_created, date_modified
	FROM Users
---------------------------------------------------------------------------*/


##**LOG IN USER**
ALTER PROC [dbo].[users_login]
	@user_login nvarchar(255)

AS

SELECT id, password, email  
FROM Users  
WHERE @user_login = email  


/*----------TEST BLOCK----------  

EXECUTE users_login  
	@user_login = 'testEmail@gmail.com'  

------------------------------*/  


##**GET ALL NOTIFICATIONS BY USER**  
ALTER PROC [dbo].[Notifications_getAllByUser]
		@id INT 
AS

SELECT * FROM Notifications 
	JOIN Notification_RecipientIds ON notification_id = id
	WHERE student_user_id = @id

/* -----TEST BLOCK-----

EXECUTE Notifications_getAllByUser 3  

-----------------------*/

##**DELETE A BLOG POST**  
ALTER PROC [dbo].[Blogs_delete] 
		@id int

AS 

DELETE FROM Blogs
WHERE id = @id

IF @@rowcount = 0
throw 51000,'Cannot delete because that post does not exist', 1


/*------TEST CODE --------

	DECLARE @id int = 10000

	EXECUTE Blogs_delete @id

-------------------------*/


##**UPDATE USER**
ALTER PROC [dbo].[users_update]
		@id INT,
		@first_name NVARCHAR(150),
		@last_name NVARCHAR(150),
		@age INT,
		@weight INT,
		@height INT,
		@email NVARCHAR(150),
		@password NVARCHAR(255)
AS

UPDATE users

SET		first_name = @first_name,
		last_name = @last_name,
		age = @age,
		weight = @weight,
		height = @height,
		email = @email,
		password = @password,
		date_modified = GETUTCDATE()

WHERE id = @id

/*------------------------------TEST CODE --------------------------
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
---------------------------------------------------------------------*/
