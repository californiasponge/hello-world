## FULL STACK EXAMPLE:

**SQL STORED PROCEDURE CREATE NEW EXERCISE**  
ALTER PROC [dbo].[exercises_insert]  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@id INT OUTPUT,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@exercise_type_id INT,   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@date_completed DATE,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@duration INT,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@description NVARCHAR(MAX),  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@user_id INT,    

AS

INSERT INTO exercises  
&nbsp;&nbsp;(exercise_type_id, date_completed, duration, description, user_id)

VALUES  
&nbsp;&nbsp;(@exercise_type_id, @date_completed, @duration, @description, @user_id)

SET  
&nbsp;&nbsp;@id = SCOPE_IDENTITY()

/* ----------------------------------------------------------TEST BLOCK-------------------------------------------------------------  

	DECLARE	@id INT,  
		@exercise_type_id INT,   
		@date_completed DATE,  
		@duration INT,  
		@description NVARCHAR(MAX),  
		@user_id INT,  
		  
	EXECUTE exercises_insert @id, @exercise_type_id, @date_completed, @duration, @description NVARCHAR(MAX), @user_id INT

	SELECT id, exercise_type_id, date_completed, duration, description, date_created, date_modified, user_id
	FROM exercises
-----------------------------------------------------------------------------------------------------------------------------------*/
