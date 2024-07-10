<script>
import {ref, defineExpose} from "vue"

  // function uploadExcluidos(){
  //     post ("http://...").then ( ()=> {
  //         $emit ("excluidos-uploaded-event")
  //     } )
  // }

  export default{

    setup(){
        const status = ref("")

        let fileToUpload = {}

        function enviarMatriculas(){
            status.value ="Enviando..." +fileToUpload.name

            let formData =  new FormData()
            formData.append("file", fileToUpload )

            //post para a API
            fetch ("http://localhost:9000/upload/matriculas-xlsx", {
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
        enviarMatriculas()
      }
        
        function limparMensagem(){
          status.value=""
        }

      defineExpose({
              limparMensagem
          })

        return {enviarMatriculas, status, handleFileUpload, limparMensagem}

    }
  }

</script>
<template>
    <div>
        status: {{status}} <br>
        
        Planilha de Matriculas 

        <input type="file" @change="handleFileUpload($event)">
  </div>
</template>
