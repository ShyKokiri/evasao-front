<script>
import {ref} from "vue"

  // function uploadExcluidos(){
  //     post ("http://...").then ( ()=> {
  //         $emit ("excluidos-uploaded-event")
  //     } )
  // }

  export default{

    setup(){
        const status = ref("")

        let fileToUpload = {}

        function enviarEgressantes(){
            status.value ="Enviando..." +fileToUpload.name

            let formData =  new FormData()
            formData.append("file", fileToUpload )

            //post para a API
            fetch ("http://localhost:9000/upload/egressos", {
              method:'POST',
              headers:{
                'Accept':'application/json'
              },
              body:formData
            }).then( (response)=>{
               console.log(response)
                return response.json()
            }).then ( (json)=>{
            
             status.value="Concluído!"
             console.log(json)
              console.log("Era pra ter json")
            })

        } 

      async  function handleFileUpload(event){
        fileToUpload =   event.target.files[0] 
        }

        return {enviarEgressantes, status, handleFileUpload}
    }
  }

</script>
<template>
    <div>
        status: {{status}} <br>
        
        Planilha de Egressantes 

        <input type="file" @change="handleFileUpload($event)">
        <button @click="enviarEgressantes()">Enviar</button>
  </div>
</template>
