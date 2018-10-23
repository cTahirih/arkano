<template>
  <header class="header">
    <h1 class="header__title">e-Ventas</h1>
  </header>
</template>

<script>
export default {
  name: 'Header',
  data () {
    return {
      name: 'Usuario'
    }
  }
}
</script>


<style scoped>
  .header {
    background-color: #3c8dbc;
    height: 8vh; 
  }

  .header__title {
    font-size: 16px;
    color: #fff;
    background-color: #367fa9;
    display: inline-flex;
    align-items: center;
    justify-items: center;
    height: inherit;
    margin: 0;
    padding: 0 20px;
  }
</style>
