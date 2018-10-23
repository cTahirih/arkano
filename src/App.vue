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
        .aside__select(
          v-show="selectMenu", 
        )
          p(
            @click="optionActive = 'data'"
          ) Estadísticas
          p(
            @click="optionActive = 'form'"
          ) Ingresar Data
      
    .main(:class="[showAsideMenu == true ? 'is-active': '']")
      .main__title
        h2.form__title  Dashboard >
        span.form__title--span(v-if="optionActive === 'form'") Nueva data
        span.form__title--span(v-else) Estadísticas
      .main__form(v-show="optionActive === 'form'")
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
      .main__overview(v-show="optionActive === 'data'")
        .overview__card.sky
          .card__body
            .card__total 
              p {{ dataDashboard.newPurchases }}
              span Nuevas Compras
            .card__icon
              img(src="../static/assets/shopping_bag.png" alt="Shopping Bag") 
          .card__footer.dark-sky
            span Más info
            i.fas.fa-arrow-circle-right
        .overview__card.green
          .card__body
            .card__total 
              p {{ dataDashboard.increasePurchases }}
              span Incremento de Compras
            .card__icon
              img(src="../static/assets/bar-chart.png" alt="Shopping Bag") 
          .card__footer.dark-green
            span Más info
            i.fas.fa-arrow-circle-right
        .overview__card.orange
          .card__body
            .card__total 
              p {{ dataDashboard.newUsers }}
              span Nuevos Usuarios
            .card__icon
              img(src="../static/assets/new_user.png" alt="Shopping Bag") 
          .card__footer.dark-orange
            span Más info
            i.fas.fa-arrow-circle-right

        .overview__card.red
          .card__body
            .card__total 
              p {{ dataDashboard.newVisits }}
              span Nuevas Visitas
            .card__icon
              img(src="../static/assets/pie_chart.png" alt="Shopping Bag") 
          .card__footer.dark-red
            span Más info
            i.fas.fa-arrow-circle-right

</template>

<script>
export default {
  name: 'Header',
  data () {
    return {
      name: 'Usuario',
      showAsideMenu: false,
      selectMenu: false,
      optionActive: 'form',
      dataDashboard: {
        newPurchases: 10,
        increasePurchases: 5,
        newUsers: 4,
        newVisits: 1
      }
    }
  },

  methods: {
    showOptionSelected() {
      console.log(this.optionSelect)
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

  .sky {
    background: #00c0ef;
  }

  .dark-sky {
    background: #00acd7;
  }

  .green {
    background: #00a65a;
  }

  .dark-green {
    background: #009551;
  }

  .orange {
    background: #f29b11;
  }

  .dark-orange {
    background: #cf850f;
  }

  .red {
    background: #dd4b39;
  }

  .dark-red {
    background: #c64333;
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

  .main__overview {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    margin: 10px 0;
  }

  .overview__card {
    width: 46.7999999999%;
    border-radius: 5px;
    margin: 0 5px;
  }

  .card__body {
    display: flex;
    justify-content: space-between;
    padding: 10px 15px;
  }

  .card__total {
    color: #fff;
    display: inline-block;
  }

  .card__total p {
    font-size: 40px;
    font-weight: bold;
    margin-bottom: 10px;
  }

  .card__total span {
    font-size: 15px;
  }

  .card__icon {
    width: 80px;
  }

  .card__footer {
    padding: 10px 15px;
    color: #fff;
    font-weight: bold;
    text-align: center;
  }

  .card__footer i {
    padding: 0 5px;
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

    .main__overview {
      flex-wrap: nowrap; 
    }

    .main__form form {
      width: 50%;
    }

    .overview__card {
      width: 25%;
    }
  }
</style>
