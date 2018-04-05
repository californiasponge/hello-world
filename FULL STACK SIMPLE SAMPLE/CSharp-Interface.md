using System.Collections.Generic;  
using MyApp.Models.Domains;  
using MyApp.Models.Requests;  

    namespace MyApp.Interfaces  
    {  
        public interface IExerciseService  
        {  
            int Create(ExerciseCreateRequest req);  
            void Delete(int id);  
            List<Exercise> GetAll();  
            Exercise GetById(int id);  
            void Update(int id, ExerciseUpdateRequest req);  
            ExerciseType GetTypeById(int id);  
            List<ExerciseType> GetAllType();  
            List<Exercise> GetAllByUser(int id);  
         }  
    }  
