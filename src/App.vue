<template lang="pug">
  #app
    header.header
      h1.header__title e-Ventas
      p.header__menu
        i.fas.fa-bars(
          @click="showAsideMenu = true",
          :class="[showAsideMenu == true ? 'is-hide': '']"
        )
        i.far.fa-window-close( 
          @click="showAsideMenu = false",
          :class="[showAsideMenu == true ? '': 'is-hide']"
      )
    aside.aside(v-show="showAsideMenu")
      .aside__user
        .user__image
          img(src="../static/assets/user.png" alt="User")
        .user__name
          p Alexander Pierce
          span
            i.fas.fa-circle.user__state
            | Online
      .aside__menu
        .asideMenu__title
          p Main navigation
        .aside__menu__buttons
          p Dashboard
          i.fas.fa-angle-down
    
</template>

<script>
export default {
  name: 'Header',
  data () {
    return {
      name: 'Usuario',
      showAsideMenu: false,
    }
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

  body {
    background-color: #ecf0f5;
  }

  *, *:before, *:after {
    box-sizing: border-box;
    margin: 0;
  }

  img{
    max-width: 100%;
  }

  .header,
  .aside__user,
  .user__image {
    display: flex;
    align-items: center;
  }

  .header {
    background-color: #3c8dbc;
    height: 8vh;
    justify-content: space-between;
  }

  .header__title {
    font-size: 16px;    
    background-color: #367fa9;    
    align-items: center;
    justify-content: center;
    height: inherit;
    margin: 0;
    padding: 0 20px;
    width: 45%;
  }

  .header__menu,
  .header__title {
    color: #fff;
    display: inline-flex;
  }

  .header__menu {
    padding-right: 20px;
  }

  .is-hide {
    display: none;
  }

  .aside {
    width: 45%;
    background: #222d32;
    color: white;
    height: 92vh;
    padding: 10px 0;
    transition: 0.5s; 
  }

  .user__image {
    width: 60px;
    padding: 0 5px;
  }

  .user__name {
    font-size: 12px;
  }

  .user__name p {
    padding: 5px 0;
  }

  .user__state {
    color: #b7d84b;
    padding-right: 3px;
    font-size: 7px;
  }

  .asideMenu__title {
    background: #1a2226;
    margin-top: 10px;
    padding: 15px 5px;
    font-weight: bold;
  }

  .aside__menu__buttons {
    display: flex;
    padding: 15px 5px;
    justify-content: space-between;
    background: #1e282c;
    border-left: 3px solid blue;
  }

  .aside__menu__buttons i {
    padding-right: 5px;
  }

  @media (min-width: 768px) {
    .header__title,
    .aside {
      width: 20%;
    }

    .user__name {
      font-size: 14px;
    }
  }
</style>
