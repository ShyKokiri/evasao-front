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

        function enviarExcluidos(){
            status.value ="Enviando..."
           
            setTimeout(() => {
              status.value ="Enviado com sucesso!"
              
            }, 3000);
        } 

        return {enviarExcluidos, status}
    }
  }

</script>
<template>
    <div>
        status: {{status}} <br>
        
        Planilha de Excluídos 

        <input type="file">
        <button @click="enviarExcluidos()">Enviar</button>
  </div>
</template>