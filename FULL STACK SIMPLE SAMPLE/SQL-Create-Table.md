## FULL STACK EXAMPLE:

**SQL QUERY TO BUILD A TABLE FOR EXERCISES**  

    USE DBNAME
    CREATE TABLE exercises (

        id int PRIMARY KEY IDENTITY(1,1) NOT NULL,
        exercise_type_id INT NOT NULL,
        date_completed DATE NOT NULL,
        duration INT NOT NULL,
        description NVARCHAR(MAX) NULL,
        user_id INT NOT NULL,
        date_created datetime2(7) DEFAULT (GETUTCDATE()) NOT NULL,
        date_modified datetime2(7) DEFAULT (GETUTCDATE()) NOT NULL

    )
