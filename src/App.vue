<template lang="pug">
  #app
    header.header
      h1.header__title e-Ventas
      .header__widget(v-cloak)
        span Temperatura:        
        span  {{ widget.temperature }}°
        .widget__icon
          img(:src="'../static/assets/icon_api/' + widget.icon + '.png'")
        span Zona Horaria:
        span  {{ widget.timezone }}
      p.header__menu
        i.fas.fa-bars(
          @click="showAsideMenu = true",
          :class="[showAsideMenu == true ? 'is-hide': '']"
        )
        i.far.fa-window-close( 
          @click="showAsideMenu = false",
          :class="[showAsideMenu == true ? '': 'is-hide']"
      )
    aside.aside(v-if="showAsideMenu")
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
        .aside__widget(v-cloak)
          span Temperatura:          
          span  {{ widget.temperature }}°
          .widget__icon
            img(:src="'../static/assets/icon_api/' + widget.icon + '.png'")
          br
          span.aside__widget Zona Horaria:          
          span  {{ widget.timezone }}
    .main(:class="[showAsideMenu == true ? 'is-active': '']")
      .main__title
        h2.form__title  Dashboard >
        span.form__title--span(v-if="optionActive === 'form'") Nueva data
        span.form__title--span(v-else) Estadísticas
      .main__form(v-show="optionActive === 'form'")
        form(v-on:submit.prevent="saveData")
          h2 Datos en Dashboard
          .form__item
            label.form__item--label Cantidad de nuevas compras
            input.form__item--input(
              type="tel", 
              required="true",
              v-model="dataValues.newPurchases",
              placeholder="Nuevas compras"
            )
          .form__item
            label.form__item--label Incremento de compras
            input.form__item--input(
              type="tel", 
              required="true",
              v-model="dataValues.increasePurchases",
              placeholder="% Incremento de compras"
            )
          .form__item
            .form__item--label Cantidad de nuevos usuarios
            input.form__item--input(
              type="tel", 
              required="true",
              v-model="dataValues.newUsers",
              placeholder="Nuevos Usuarios"
            )
          .form__item
            label.form__item--label Cantidad nuevas visitas
            input.form__item--input(
              type="tel", 
              required="true",
              v-model="dataValues.newVisits",
              placeholder="Nuevas Visitas"
            )
          .form__item.button
            button.form__item--button(type="submit") Ingresar Datos
      .main__overview(v-show="optionActive === 'data'")
        .overview__card.sky
          .card__body
            .card__total 
              p {{ dataCards.newPurchases }}
              span Nuevas Compras
            .card__icon
              img(src="../static/assets/shopping_bag.png" alt="Shopping Bag") 
          .card__footer.dark-sky
            span Más info
            i.fas.fa-arrow-circle-right
        .overview__card.green
          .card__body
            .card__total 
              p {{ dataCards.increasePurchases }}%
              span Incremento de Compras
            .card__icon
              img(src="../static/assets/bar-chart.png" alt="Shopping Bag") 
          .card__footer.dark-green
            span Más info
            i.fas.fa-arrow-circle-right
        .overview__card.orange
          .card__body
            .card__total 
              p {{ dataCards.newUsers }}
              span Nuevos Usuarios
            .card__icon
              img(src="../static/assets/new_user.png" alt="Shopping Bag") 
          .card__footer.dark-orange
            span Más info
            i.fas.fa-arrow-circle-right

        .overview__card.red
          .card__body
            .card__total 
              p {{ dataCards.newVisits }}
              span Nuevas Visitas
            .card__icon
              img(src="../static/assets/pie_chart.png" alt="Shopping Bag") 
          .card__footer.dark-red
            span Más info
            i.fas.fa-arrow-circle-right

</template>

<script>
import axios from 'axios';
export default {
  name: 'Header',
  data () {
    return {
      name: 'Usuario',
      showAsideMenu: false,
      selectMenu: false,
      optionActive: 'data',
      dataValues: {
        newPurchases: null,
        increasePurchases: null,
        newUsers: null,
        newVisits: null
      },
      dataCards: {
        newPurchases: 10,
        increasePurchases: 12,
        newUsers: 9,
        newVisits: 3
      },
      widget: {
        timezone: '',
        temperature: '',
        icon: ''
      }
    }
  },

  mounted() {
    var ele = document.querySelectorAll('.form__item--input')[0];
    ele.onkeypress = function(e) {
      if(isNaN(this.value+String.fromCharCode(e.charCode)))
          return false;
    }
    ele.onpaste = function(e){
      e.preventDefault();
    }

    this.getLocationKey();
  },

  methods: {
    saveData() {
      this.optionActive = 'data';
      this.dataCards.newPurchases = this.dataCards.newPurchases + parseInt(this.dataValues.newPurchases);
      this.dataCards.increasePurchases = this.dataCards.increasePurchases + parseInt(this.dataValues.increasePurchases);
      this.dataCards.newUsers = this.dataCards.newUsers + parseInt(this.dataValues.newUsers);
      this.dataCards.newVisits = this.dataCards.newVisits + parseInt(this.dataValues.newVisits);

      this.dataValues.newPurchases = null;
      this.dataValues.increasePurchases = null;
      this.dataValues.newUsers = null;
      this.dataValues.newVisits = null;
    },

    getLocationKey() {

      if (navigator.geolocation) {      
        navigator.geolocation.getCurrentPosition((position) => {
          let myLocation = { 
            lat: position.coords.latitude, 
            lng: position.coords.longitude 
          };

          let proxy = 'https://cors-anywhere.herokuapp.com/';
          let apiURL = `https://cors-anywhere.herokuapp.com/https://api.darksky.net/forecast/133ef44c6b580d317343f1b7dca221e0/${myLocation.lat},${myLocation.lng}?units=si`;

          let url = proxy + apiURL;

          axios.get(url)
            .then(response => {
              let res = response.data;
              this.widget.temperature = res.currently.temperature;
              this.widget.icon = res.currently.icon;
              this.widget.timezone = res.timezone;          
            })
            .catch(e => {
              console.log(e);
            })
        });
      } else {
        console.log('Geolocation is not supported by this browser.');
      }
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
    font-family: 'gotham_book', 'sans-serif';
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

  [v-cloak] {
    display: none;
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

  .header__widget {
    display: none;
    color: #fff;
    text-align: left;
    width: 50%;
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

  .aside__widget {
    display: block;
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
  }

  .aside__menu__buttons i {
    padding-right: 5px;
    cursor: pointer;
  }

  .aside__select p {
    padding: 10px 5px;
    border-bottom: 1px solid #d9d9d9;
    cursor: pointer;
  }

  .aside__select p:hover {
    background: #3c8dbc;
  }

  .widget__icon {
    width: 40px;
    display: inline-flex;
    align-items: center;
    padding: 0 5px;

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
    margin: 5px;
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

    .header__widget {
      display: block;
    }

    .aside__widget {
      display: none;
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
