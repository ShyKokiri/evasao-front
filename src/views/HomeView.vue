<script setup lang="ts">
  import EgressantesUpload from "../components/EgressantesUpload.vue" 
  import ExcluidosUpload from "../components/ExcluidosUpload.vue"
  import MatriculaUpload from "../components/MatriculaUpload.vue"
  import IngressantesUpload from "../components/IngressantesUpload.vue"
  import Resultado from "../components/Resultado.vue"
  import {ref} from "vue"



  // export default{
  //   setup(){
  //     const egressantesUploaded = ref( false)
  //     const ingressantesUploaded = ref (false) 
  //     const excluidosUploaded = ref (false) 
  //     const matriculaUploaded = ref (false)

  //     return (egressantesUploaded, ingressantesUploaded, excluidosUploaded, matriculaUploaded)
  //   }

  // }


  // on( "excluidos-uploaded-event", ()=>{
  //   excluidosUploaded= true
  // })


  // function habilitarCalculo(){
  //  return excluidosUploaded && ingressantesUploaded && egressantesUploaded && matriculaUploaded
  // }

  //   function calcularEvasao(){
  //       get ("/calc").then ( (dado)=>{

  //         dados = ///resultado 
  //       })
  //   }
</script>

<template>
  <main>

  <div class="planilhas">
     

    <EgressantesUpload  />

    <ExcluidosUpload/> 

    <MatriculaUpload/>

    <IngressantesUpload/>

    <Resultado/>
    
    <!-- <div>
    <button :enable="habilitarCalculo()" @click="calcularEvasao()"> Calcular Evasão</button>
    </div>  -->
     <button > Calcular Evasão</button> 
  
  </div>

  </main>
</template>
<style>

.planilhas{
  display: flex;
  flex-direction: column;
  

}
.planilhas> div{
  padding: 0.5em;

  }

</style>