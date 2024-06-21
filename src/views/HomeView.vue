<script setup lang="ts">
import EgressantesUpload from "../components/EgressantesUpload.vue"
import ExcluidosUpload from "../components/ExcluidosUpload.vue"
import MatriculaUpload from "../components/MatriculaUpload.vue"
import IngressantesUpload from "../components/IngressantesUpload.vue"
import Resultado from "../components/Resultado.vue"
import { ref } from "vue"

const localEgressantes = ref(null)
const localIngressantes = ref(null)
const localExcluidos = ref(null)
const localMatriculas = ref(null)


function calcularEvasao() {

  fetch("http://localhost:9000/upload/calc", {
    method: 'GET',
    headers: {
      'Accept': 'application/json'
    },

  }).then((response) => {
    return { json: response.json(), status: response.status }
  }).then((result) => {
    if (result.status == 500) {
      result.json.then(j => {
        alert(j.erro)
      })
    }

    localEgressantes.value.limparMensagem()
    localIngressantes.value.limparMensagem()
    localExcluidos.value.limparMensagem()
    localMatriculas.value.limparMensagem()
  })
}

</script>

<template>
  <main>

    <div class="planilhas">


      <EgressantesUpload ref="localEgressantes" />

      <IngressantesUpload ref="localIngressantes"/>

      <MatriculaUpload ref="localMatriculas"/>

      <ExcluidosUpload ref="localExcluidos"/>

      <Resultado />


      <button @click="calcularEvasao()"> Calcular Evasão</button>
    </div>


  </main>
</template>
<style>
.planilhas {
  display: flex;
  flex-direction: column;


}

.planilhas>div {
  padding: 0.5em;

}
</style>