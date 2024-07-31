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

  fetch("http://localhost:9000/upload/calc?curso=CIÊNCIA DA COMPUTAÇÃO - BACHARELADO", {
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
            <br>
          <button @click="calcularEvasao()" > Calcular Evasão</button>

        </div>
        <div class="resultado-container">
          <Resultado :result="resultadoCalculado" :show="resultadoCalculado.length > 0" />
        </div>
    </div>
  </main>
</template>
<style>/* Ajustes adicionais para garantir que não haja sobreposição */
#container {

  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  width: 100%;
  align-items: flex-start; /* Alinha os itens ao início, evitando esticamento */
}

#container > div {
  padding: 1em;
  flex: 1 1 250px; /* Ajusta flex-grow, flex-shrink e flex-basis */
  box-sizing: border-box; /* Garante que padding seja incluído no cálculo da largura */
}

.resultado-container {
  flex-basis: 100%;
  display: flex;
  justify-content: center;
  overflow-x: auto; /* Adiciona rolagem horizontal se necessário */
}

@media (max-width: 768px) {
  #container {
    flex-direction: column; /* Muda para layout de coluna em telas menores */
  }
}
</style>