<template>
  <div id="app" class="container">
         <p class="text-center">Welcome to tax calculator</p>
         <SalesTax />
       

  </div>
</template>

<script>

import SalesTax from './components/SalesTax.vue'

export default {
  name: 'App',
  components: {
       SalesTax,
  
  }
}
</script>

<style>
p{
  font-family: 'Times New Roman', Times, serif;
  font-size: 40px;
}
</style>
