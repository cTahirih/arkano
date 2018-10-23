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
          i.fas.fa-angle-down(
            @click="selectMenu = true",
            :class="[selectMenu == true ? 'is-hide': '']"
          )
          i.fas.fa-angle-up( 
            @click="selectMenu = false",
            :class="[selectMenu == true ? '': 'is-hide']"
          )
        transition(name="fade")
          .aside__select(v-show="selectMenu")
            p Estadísticas
            p Ingresar data
      
    .main(:class="[showAsideMenu == true ? 'is-active': '']")
      .main__title
        h2.form__title  Dashboard >
        span.form__title--span Nueva data
      .main__form
        form
          h2 Datos en Dashboard
          .form__item
            label.form__item--label Cantidad de nuevas compras
            input.form__item--input(
              type="tel", 
              required="true",
              placeholder="Nuevas compras"
            )
          .form__item
            label.form__item--label Incremento de compras
            input.form__item--input(
              type="tel", 
              required="true",
              placeholder="% Incremento de compras"
            )
          .form__item
            .form__item--label Cantidad de nuevos usuarios
            input.form__item--input(
              type="tel", 
              required="true",
              placeholder="Nuevos Usuarios"
            )
          .form__item
            label.form__item--label Cantidad nuevas visitas
            input.form__item--input(
              type="tel", 
              required="true",
              placeholder="Nuevas Visitas"
            )
          .form__item.button
            button.form__item--button Ingresar Datos
    
</template>

<script>
export default {
  name: 'Header',
  data () {
    return {
      name: 'Usuario',
      showAsideMenu: false,
      selectMenu: false,
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
    color: #1e282c;
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

  .is-active {
    width: 100%!important;
  }



  .aside {
    width: 45%;
    background: #222d32;
    color: white;
    height: 92vh;
    padding: 10px 0;
    display: inline-block;
    transition: 0.5s;
    position: fixed;
    z-index: 1000;
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
    border-left: 3px solid #3c8dbc;
    cursor: pointer;
  }

  .aside__menu__buttons i {
    padding-right: 5px;
  }

  .aside__select p {
    padding: 10px 5px;
    border-bottom: 1px solid #d9d9d9;
    cursor: pointer;
  }

  .aside__select p:hover {
    background: #3c8dbc;
  }

  .main {
    min-height: 92vh;
    display: inline-block;
    position: absolute;
    padding: 10px 20px;
    width: 100%; 
  }

  .main__form {
    display: flex;
    justify-content: center;
  }

  .main__form form {
    background: #fff;
    padding: 10px 20px;
    border-radius: 10px;
    margin: 10px 0;
    width: 100%;
  }

  .form__title {
    display: inline-block;
    padding-right: 5px;
    font-size: 20px;
  }

  .form__title--span {
    font-size: 20px;
  }

  .form__item--label {
    display: block;
  }

  .form__item {
    margin: 10px 0;
  }

  .form__item--label {
    font-size: 15px;
    font-weight: bold;
    padding-bottom: 10px;
    color: #367fa9;
  }

  .form__item--input {
    background: inherit;
    border-radius: 5px;
    padding: 5px;
    border: 2px solid #3c8dbc;
    font-family: inherit;
    width: 100%;
  }

  .form__item--input:focus {
    outline: none;
    border: 2px solid #44accf;
  }

  .form__item.button {
    display: flex;
    justify-content: end;
  }

  .form__item--button {
    background: #367fa9;
    border-radius: 5px;
    padding: 10px 5px;    
    font-size: 15px;
    color: #fff;
    border: none;
    font-weight: bold;
  }

  @media (min-width: 768px) {
    .header__title,
    .aside {
      width: 20%;
    }

    .user__name {
      font-size: 14px;
    }

    .aside {
      position: relative;
    }

    .is-active {
      width: 80%!important;
    }

    .main__form form {
      width: 50%;
    }
  }
</style>
