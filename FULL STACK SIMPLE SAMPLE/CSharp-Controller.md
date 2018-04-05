## FULL STACK EXAMPLE  
**THIS SAMPLE ASSUMES REFERENCE TO Unity.AspNet.WebApi, Microsoft.AspNet.Cors NuGet Packages**  

using MyApp.Interfaces;  
using MyApp.Models.Domains;  
using MyApp.Models.Requests;  
using System.Collections.Generic;  
using System.Net;  
using System.Net.Http;  
using System.Web.Http;  
using System.Web.Http.Cors;  

    namespace MyApp.Controllers  
    {  
        [Authorize]  
        [RoutePrefix("api/exercises")]  
        [EnableCors(origins: "http://192.168.1.109:19001", headers:"*", methods:"*")]  
        public class ExercisesController : ApiController  
        {  
            readonly IExerciseService exerciseService;  

            public ExercisesController(IExerciseService exerciseService)  
            {  
                this.exerciseService = exerciseService;  
            }  
            
            [HttpPost, Route("new-exercise")]  
            public HttpResponseMessage Insert(ExerciseCreateRequest req)   
            {
                if (!ModelState.IsValid)  
                {  
                    return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);  
                }  
                req.UserId = int.Parse(User.Identity.Name);  

                int newId = exerciseService.Create(req);  

                return Request.CreateResponse(HttpStatusCode.Created, newId);  

            }  
        }  
    }  
