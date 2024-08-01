<script setup lang="ts">
// @ts-ignore
import EgressantesUpload from "../components/EgressantesUpload.vue"
import ExcluidosUpload from "../components/ExcluidosUpload.vue"
import MatriculaUpload from "../components/MatriculaUpload.vue"
import IngressantesUpload from "../components/IngressantesUpload.vue"
import Resultado from "../components/Resultado.vue"
import { ref } from "vue"

const localEgressantes = ref<any>(null)
const localIngressantes = ref<any>(null)
const localExcluidos = ref<any>(null)
const localMatriculas = ref<any>(null)
const resultadoCalculado = ref([])
const cursoSelecionado = ref('')


const cursos = ref ( new Set(  ['ADMINISTRAÇÃO - BACHARELADO',
'ADMINISTRAÇÃO - BACHARELADO',
'ADMINISTRAÇÃO - BACHARELADO',
'ADMINISTRAÇÃO - BACHARELADO',
'ADMINISTRAÇÃO - BACHARELADO',
'ANÁLISE DE SISTEMAS - BACHARELADO',
'ARQUITETURA E URBANISMO - BACHARELADO',
'ARTES VISUAIS - BACHARELADO -  HAB. EM ARTES PLÁSTICAS',
'ARTES VISUAIS - LICENCIATURA - HAB. EM ARTES PLÁSTICAS',
'CIÊNCIA DA COMPUTAÇÃO - BACHARELADO',
'CIÊNCIAS BIOLÓGICAS - BACHARELADO',
'CIÊNCIAS BIOLÓGICAS - LICENCIATURA',
'CIÊNCIAS BIOLÓGICAS - LICENCIATURA',
'CIÊNCIAS BIOLÓGICAS - LICENCIATURA',
'CIÊNCIAS CONTÁBEIS - BACHARELADO',
'CIÊNCIAS CONTÁBEIS - BACHARELADO',
'CIÊNCIAS CONTÁBEIS - BACHARELADO',
'CIÊNCIAS ECONÔMICAS - BACHARELADO',
'CIÊNCIAS SOCIAIS - BACHARELADO',
'COMUNICAÇÃO SOCIAL - HABILITAÇÃO EM JORNALISMO',
'CURSO DE LICENCIATURA EM PEDAGOGIA PARA EDUCAÇÃO INFANTIL',
'DIREITO - BACHARELADO',
'DIREITO - BACHARELADO',
'DIREITO - BACHARELADO',
'DIREITO - BACHARELADO',
'DIREITO - BACHARELADO',
'EDUCAÇÃO FÍSICA - LICENCIATURA',
'ENFERMAGEM - BACHARELADO',
'ENFERMAGEM - BACHARELADO',
'ENGENHARIA AMBIENTAL - BACHARELADO',
'ENGENHARIA CIVIL - BACHARELADO',
'ENGENHARIA ELÉTRICA - BACHARELADO',
'FARMÁCIA - BACHARELADO',
'FARMÁCIA-BIOQUÍMICA - HABILITAÇÃO EM ANÁLISES CLÍNICAS',
'FARMÁCIA-BIOQUÍMICA - HABILITAÇÃO EM TECNOLOGIA DE ALIMENTOS',
'FÍSICA - BACHARELADO',
'FÍSICA - LICENCIATURA',
'GEOGRAFIA - BACHARELADO',
'GEOGRAFIA - BACHARELADO',
'GEOGRAFIA - LICENCIATURA',
'GEOGRAFIA - LICENCIATURA',
'GEOGRAFIA - LICENCIATURA',
'HISTÓRIA - LICENCIATURA',
'HISTÓRIA - LICENCIATURA',
'HISTÓRIA - LICENCIATURA',
'HISTÓRIA - LICENCIATURA',
'LETRAS - LICENCIATURA - HABILITAÇÃO EM PORTUGUÊS/ESPANHOL',
'LETRAS - LICENCIATURA - HABILITAÇÃO EM PORTUGUÊS/ESPANHOL',
'LETRAS - LICENCIATURA - HABILITAÇÃO EM PORTUGUÊS/ESPANHOL',
'LETRAS - LICENCIATURA - HABILITAÇÃO EM PORTUGUÊS/INGLÊS',
'LETRAS - LICENCIATURA - HABILITAÇÃO EM PORTUGUÊS/INGLÊS',
'LETRAS - LICENCIATURA - HABILITAÇÃO EM PORTUGUÊS/INGLÊS',
'LETRAS - LICENCIATURA - HABILITAÇÃO EM PORTUGUÊS/INGLÊS E RESPECTIVAS LITERATURAS',
'LETRAS - LICENCIATURA - HABILITAÇÃO EM PORTUGUÊS/INGLÊS E RESPECTIVAS LITERATURAS',
'LETRAS - LICENCIATURA - HABILITAÇÃO EM PORTUGUÊS/LITERATURA',
'LETRAS - LICENCIATURA - HABILITAÇÃO EM PORTUGUÊS/LITERATURA',
'MATEMÁTICA - BACHARELADO',
'MATEMÁTICA - LICENCIATURA',
'MATEMÁTICA - LICENCIATURA',
'MATEMÁTICA - LICENCIATURA',
'MATEMÁTICA - LICENCIATURA',
'MEDICINA - BACHARELADO',
'MEDICINA VETERINÁRIA - BACHARELADO',
'ODONTOLOGIA - BACHARELADO',
'PEDAGOGIA - LICENCIATURA',
'PEDAGOGIA - LICENCIATURA',
'PEDAGOGIA - LICENCIATURA',
'PEDAGOGIA - LICENCIATURA - HAB. EM EDUCAÇÃO INFANTIL',
'PEDAGOGIA - LICENCIATURA - HAB. EM EDUCAÇÃO INFANTIL',
'PEDAGOGIA - LICENCIATURA - HAB. EM SÉRIES INICIAIS DO ENSINO FUNDAMENTAL',
'PEDAGOGIA - LICENCIATURA - HAB. EM SÉRIES INICIAIS DO ENSINO FUNDAMENTAL',
'PEDAGOGIA - LICENCIATURA - HAB. EM SÉRIES INICIAIS DO ENSINO FUNDAMENTAL',
'PEDAGOGIA - LICENCIATURA - HABILITAÇÃO EM EDUCAÇÃO INFANTIL',
'PEDAGOGIA - LICENCIATURA PLENA - HABILITAÇÃO EM FORMAÇÃO DE PROFESSORES PARA OS',
'PSICOLOGIA  - BACHARELADO',
'PSICOLOGIA - BACHARELADO',
'QUÍMICA - BACHARELADO EM QUÍMICA TECNOLÓGICA',
'QUÍMICA - LICENCIATURA',
'SISTEMAS DE INFORMAÇÃO - BACHARELADO',
'TURISMO - BACHARELADO',
'ZOOTECNIA - BACHARELADO'
]))

function calcularEvasao() {

  if (cursoSelecionado.value == '') {
    alert('Selecione um curso')
    return
  }
  
   fetch(`http://localhost:9000/upload/calc?curso=${cursoSelecionado.value}`, {
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

    localEgressantes?.value?.limparMensagem()
    localIngressantes?.value?.limparMensagem()
    localExcluidos?.value?.limparMensagem()
    localMatriculas?.value?.limparMensagem()
  })
}

</script>

<template>
  <main>
    <div id="container">
        <div class="planilhas">
          <select id="sel-curso" v-model="cursoSelecionado">
            <option value="">Selecione um curso</option>
            <option  v-for="c in cursos" :key="c" :value='c'>{{c}}</option>
      </select>

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