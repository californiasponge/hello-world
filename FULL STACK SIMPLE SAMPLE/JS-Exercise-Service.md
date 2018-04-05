## FULL STACK EXAMPLE  
**Assumes C# files share same IP address due to IIS configuration to deal with CORS**  
**This sample contains functions that were not defined in the C# files**  
    
    import * as axios from 'axios';

    const exerciseUrl = 'http://000.000.0.000/api/exercises/';

    //EXERCISE SERVICES********************************//
        export function createExercise(exerciseData) {
            const url = exerciseUrl + 'new-exercise'; 

            return axios.post(url, exerciseData)
        }

        export function getExerciseTypes() {
            const url = exerciseUrl + "exercise-type";

            return axios.get(url)
        }

        export function getExerciseTypeId(id) {
            const url = exerciseUrl + 'exercise-type' + id;

            return axios.get(url, id)
        }
