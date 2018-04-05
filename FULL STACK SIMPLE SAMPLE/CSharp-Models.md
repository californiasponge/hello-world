##FULL STACK EXAMPLE  

using System;  
using System.ComponentModel.DataAnnotations;  

    namespace MyApp.Models.Requests  
    {  
        public class ExerciseCreateRequest  
        {  
            [Required]  
            public int? ExerciseTypeId { get; set; }  
            [Required]  
            public int? UserId { get; set; }  
            [Required]  
            public DateTime DateCompleted { get; set; }  
            [Required]  
            public int? Duration { get; set; }  
            public string Description { get; set; }  
        }  
    }

************************************************************************************************************************

using System;  

    namespace MyApp.Models.Domains  
    {  
        public class Exercise  
        {  
            public int? Id { get; set; }  
            public int? ExerciseTypeId { get; set; }  
            public DateTime DateCompleted { get; set; }  
            public int? Duration { get; set; }  
            public string Description { get; set; }  
            public DateTime DateCreated { get; set; }  
            public DateTime DateModified { get; set; }  
        }  
    }  
