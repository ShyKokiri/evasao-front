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

  flex-direction: column; /* Adicionado para garantir centralização vertical */
}

main {
  display: flex;
  flex-direction: column;
  align-items: center; /* Garante que os itens de main estejam centralizados horizontalmente */
  text-align: center; /* Centraliza o texto e elementos inline dentro de main */
}

/* Se necessário, ajuste o estilo de .logo para garantir que a imagem também esteja centralizada */
.logo {
  display: block; /* Faz a imagem se comportar como um bloco para respeitar o alinhamento */
  margin: 0 auto; /* Adiciona margem automática dos lados para centralizar horizontalmente */
}
</style>