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
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  flex-direction: column; /* Adicionado para garantir centralização vertical */
}

main {
  display: flex;
  flex-direction: column;
  align-items: left; /* Garante que os itens de main estejam centralizados horizontalmente */
  text-align: left; /* Centraliza o texto e elementos inline dentro de main */
}
main div {
  text-align: left;
  
}

</style>