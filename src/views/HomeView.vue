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
const resultadoCalculado = ref([])

function calcularEvasao() {

  fetch("http://localhost:9000/upload/calc", {
    method: 'GET',
    headers: {
      'Accept': 'application/json'
    },

  }).then((response) => {
    return { json: response.json(), status: response.status }
  }).then(async(result) => {
    if (result.status == 500) {
      result.json.then(j => {
        alert(j.erro)
      })
    }
    else {
      const r = await result.json
      console.log(r)

      //alimentar um array
      resultadoCalculado.value = r
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
    <div id="container">
        <div class="planilhas">

          <EgressantesUpload ref="localEgressantes" />

          <IngressantesUpload ref="localIngressantes" />

          <MatriculaUpload ref="localMatriculas" />

          <ExcluidosUpload ref="localExcluidos" />

          <button @click="calcularEvasao()" > Calcular Evasão</button>

        </div>
        <div>
          <Resultado :result="resultadoCalculado" :show="resultadoCalculado.length > 0" />
        </div>
    </div>
  </main>
</template>
<style>
#container{
  display: flex;
  flex-direction: row;
} 
.planilhas {
  display: flex;
  flex-direction: column;
}

.planilhas>div {
  padding: 0.5em;

}
</style>