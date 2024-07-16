<script setup>
</script>

<template>
  <div class="container">
    <main>
      <div>
        <img class="logo" src="./assets/grafo_facom.png" alt="Vue logo" />
        <h1>Sistema de Calculo de Evasão</h1>
      </div>
      <div>
        <RouterView />
      </div>
    </main>
  </div>
</template>
<style scoped>

.container {
  width: 100%; /* Estica o container para ocupar 100% da largura da viewport */
  height: 100vh; /* Estica o container para ocupar 100% da altura da viewport */
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: gray;
  flex-direction: column;
}

main {
  display: flex;
  flex-direction: column;
  align-items: center; /* Garante que os itens de main estejam centralizados horizontalmente */
  text-align: center; /* Centraliza o texto e elementos inline dentro de main */
}

.logo {
  display: block; /* Faz a imagem se comportar como um bloco para respeitar o alinhamento */
  margin: 0 auto; /* Adiciona margem automática dos lados para centralizar horizontalmente */
}
</style>