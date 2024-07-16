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

        function enviarExcluidos(){
            status.value ="Enviando..." +fileToUpload.name

            let formData =  new FormData()
            formData.append("file", fileToUpload )

            //post para a API
            fetch ("http://localhost:9000/upload/excluidos", {
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
        enviarExcluidos()
      }

        function limparMensagem(){
          status.value=""
        }

      defineExpose({
              limparMensagem
          })

        return {enviarExcluidos, status, handleFileUpload, limparMensagem}

    }
  }

</script>
<template>
  <div class="planilhas">

    <h2>Upload de Excluídos</h2>

    <input type="file" @change="handleFileUpload($event)">
    <div>status: {{status}} </div>
      
</div>
</template>
<style scoped>
.planilhas{
  display: flex;
  flex-direction: column;
  align-items: left; /* Garante que os itens de main estejam centralizados horizontalmente */
  text-align: left; /* Centraliza o texto e elementos inline dentro de main */
}
</style>