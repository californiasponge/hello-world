##FULL STACK EXAMPLE  
**THIS SAMPLE INTENTIONALLY HAS COMMENTED OUT METHODS NOT IMPLEMENTED IN THE CSharp-Services.md FILE**  
**METHODS ARE LEFT TO DEMONSTRATE A MORE REALISTIC INTERFACE BUT COMMENTED OUT FOR ACCURACY WITH CURRENT AVAILABLE FILES**  

using System.Collections.Generic;  
using MyApp.Models.Domains;  
using MyApp.Models.Requests;  

    namespace MyApp.Interfaces  
    {  
        public interface IExerciseService  
        {  
            int Create(ExerciseCreateRequest req);  
            //void Delete(int id);  
            //List<Exercise> GetAll();  
            //Exercise GetById(int id);  
            //void Update(int id, ExerciseUpdateRequest req);  
            //ExerciseType GetTypeById(int id);  
            //List<ExerciseType> GetAllType();  
            //List<Exercise> GetAllByUser(int id);  
         }  
    }  
