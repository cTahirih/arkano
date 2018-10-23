<template>
  <div id="app">
    <Header/>
  </div>
</template>

<script>
import Header from './components/Header'

export default {
  name: 'App',
  components: {
    Header
  }
}
</script>

<style>
  @font-face {
    font-family: 'gotham_book';
    src: url('../static/fonts/gotham-Book.woff') format('woff');
    font-weight: normal;
    font-style: normal;
  }
  @font-face {
    font-family: 'garamont-Regular.woff';
    src: url('../static/fonts/garamont-Regular.woff') format('woff');
    font-weight: normal;
    font-style: normal;
  }
  html {
    font-family: 'gotham_book';
    font-size: 16px;
    word-spacing: 1px;
    -ms-text-size-adjust: 100%;
    -webkit-text-size-adjust: 100%;
    -moz-osx-font-smoothing: grayscale;
    -webkit-font-smoothing: antialiased;
    box-sizing: border-box;
  }

  *, *:before, *:after {
    box-sizing: border-box;
    margin: 0;
  }

  img{
    max-width: 100%;
  }
</style>
