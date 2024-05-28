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

        function enviarExcluidos(){
            status.value ="Enviando..." +fileToUpload.name

            let formData =  new FormData()
            formData.append("file", fileToUpload )

            //post para a API
            fetch ("http://localhost:9000/upload/excluidos", {
              method:'POST',
              headers:{
                'Accept':'application/json', 
                'Content-type':'multipart/form-data'
              },
              body:formData
            }).then( (response)=>{
                return response.json()
            }).then ( (json)=>{
              status.value="Concluído!"
              console.log(json)
            })

        } 

      async  function handleFileUpload(event){
        fileToUpload =   event.target.files[0] 



        }

        return {enviarExcluidos, status, handleFileUpload}
    }
  }

</script>
<template>
    <div>
        status: {{status}} <br>
        
        Planilha de Excluídos 

        <input type="file" @change="handleFileUpload($event)">
        <button @click="enviarExcluidos()">Enviar</button>
  </div>
</template>