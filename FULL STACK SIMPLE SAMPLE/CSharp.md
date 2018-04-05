##FULL STACK EXAMPLE:  
**This sample has reference to a NuGet package called BCrypt.Net-Next**  
**This sample does not make use of wrappers or extension methods**  

using Namespace.Models.Interfaces;  
using Namespace.Models.Domains;  
using Namespace.Models.Requests;  
using System.Collections.Generic;  
using System.Configuration;  
using System.Data.SqlClient;  
using System.Data;  

    namespace MyApp.Services  
    {  
      public class ExercisesService : IExerciseService  
       {  
         public int Create(ExerciseCreateRequest req)  
         {  
            using (var con = new SqlConnection(ConfigurationManager.ConnectionStrings["NamedConnection"].ConnectionString))  
             {   
                con.Open();  

                var cmd = con.CreateCommand();  

                cmd.CommandText = "exercises_insert";  
                cmd.CommandType = CommandType.StoredProcedure;  

                cmd.Parameters.AddWithValue("@user_id", req.UserId);
                cmd.Parameters.AddWithValue("@exercise_type_id", req.ExerciseTypeId);
                cmd.Parameters.AddWithValue("@date_completed", req.DateCompleted);
                cmd.Parameters.AddWithValue("@duration", req.Duration);
                cmd.Parameters.AddWithValue("@description", req.Description ?? (object)DBNull.Value);
                cmd.Parameters.Add("@id", SqlDbType.Int).Direction = ParameterDirection.Output;

                cmd.ExecuteNonQuery();

                int newId = (int)cmd.Parameters["@id"].Value;

                return newId;
              }
           }
        }
    }
