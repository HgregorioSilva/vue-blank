<template>
  <div id="app" class="container">
    <div id="nav" class="row text-center">
      <router-link to="/">Home</router-link> |
      <router-link to="/motos">Motos</router-link> |
      <router-link to="/atualizar">Atualizar moto</router-link> |
      <router-link to="/deletar">Deletar moto</router-link> |
      <router-link to="/login">Login</router-link> 
    </div>
    <router-view />
  </div>
</template>