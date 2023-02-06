<template>
  <div class="app">
    <header class="header">
      <div class="header__container container">
        <a href="index.html" class="header__logo">URL SHORTENER</a>
      </div>
    </header>
    <main class="main">
      <div class="shorten">
        <div class="shorten__container container">
          <h1 class="shorten__title">Paste the URL to be shortened</h1>
          <div class="shorten__search">
            <input placeholder="Example: https://google.com" v-model="link" type="text" class="shorten__search-input">
            <button @click="shorten" class="shorten__search-button">Shrink</button>
          </div>
          <p class="shorten__result" v-if="shortenedLink">
            <a target="_blank" class="shorten__result-link" :href="shortenedLink.result_url">{{
              shortenedLink.result_url
            }}</a>
          </p>
          <p class="shorten__subtitle">Url Shortened is a free tool to shorten a URL. Use URL Shortener to create a
            shortned link and use it anywere</p>
        </div>
      </div>
      <div class="advantages">
        <div class="advantages__container container">
          <div class="advantages__item" v-for="advantage in advantages" :key="advantage.title">
            <div class="advantages__item-img">
              <img :src="require(`@/assets/${advantage.img}`)" alt="">
            </div>
            <div class="advantages__item-title">{{ advantage.title }}</div>
            <div class="advantages__item-subtitle">{{ advantage.description }}</div>
          </div>
        </div>
      </div>
    </main>
    <footer class="footer">
      <div class="footer__container container">
        <p class="footer__creator">Создатель: Азизбек Абибуллаев</p>
        <p class="footer__creator">Дизайнер: Фаррух Мирмахмудов</p>
        <p class="footer__creator">Спонсор: Маершин Глеб</p>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      advantages: [
        { img: "easy.png", title: "EASY", description: "URL SHORTENER IS EASY AND FAST AND EFFECTIVE WAY TO SHORTEN YOUR LONG URLS" },
        { img: "shortened.png", title: "Shortened", description: "Any links can be shortener with powerful algorithms" },
        { img: "secure.png", title: "Secure", description: "With hugh level encryption your urls are always safe and secure with https" },
        { img: "stonks.png", title: "Statistics", description: "You can see stats on how many users have used your shortened urt" },
        { img: "reliable.png", title: "Reliable", description: "We delete any links which is a potential threat tomalware or viruses" },
        { img: "devices.png", title: "Devices", description: "Compatible with smartphones, tablets and desktops" },
      ],
      link: "",
      shortenedLink: "",
      regex: new RegExp("^(http|https)://")
    }
  },
  methods: {
    shorten() {
      if (this.regex.test(this.link)) {
        const encodedParams = new URLSearchParams();
        encodedParams.append("url", "https://google.com/");

        const options = {
          method: 'POST',
          headers: {
            'content-type': 'application/x-www-form-urlencoded',
            'X-RapidAPI-Key': '5810ad3a68msha556f21af7078b7p1ad301jsn2883347bbc21',
            'X-RapidAPI-Host': 'url-shortener-service.p.rapidapi.com'
          },
          body: encodedParams
        };

        fetch('https://url-shortener-service.p.rapidapi.com/shorten', options)
          .then(response => response.json())
          .then(response => this.shortenedLink = response)
          .catch(err => console.error(err));
      }
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');


* {
  padding: 0px;
  margin: 0px;
  border: none;
}

*,
*::before,
*::after {
  box-sizing: border-box;
}

:focus,
:active {}

a:focus,
a:active {}



a,
a:link,
a:visited {
  text-decoration: none;
}

a:hover {
  text-decoration: none;
}



aside,
nav,
footer,
header,
section,
main {
  display: block;
}

h1,
h2,
h3,
h4,
h5,
h6,
p {
  font-size: inherit;
  font-weight: inherit;
}

ul,
ul li {
  list-style: none;
}

img {
  vertical-align: top;
}

img,
svg {
  max-width: 100%;
  height: auto;
}

address {
  font-style: normal;
}

input,
textarea,
button,
select {
  font-family: inherit;
  font-size: inherit;
  color: inherit;
  background-color: transparent;
}

input::-ms-clear {
  display: none;
}

button,
input[type="submit"] {
  display: inline-block;
  box-shadow: none;
  background-color: transparent;
  background: none;
  cursor: pointer;
}

input:focus,
input:active,
button:focus,
button:active {
  outline: none;
}

button::-moz-focus-inner {
  padding: 0;
  border: 0;
}

label {
  cursor: pointer;
}

legend {
  display: block;
}

body {
  height: 100vh;
}

#app {
  height: 100%;
}

.app {
  display: flex;
  flex-direction: column;
  min-height: 100%;
}

.container {
  max-width: 900px;
  margin: 0 auto;
  padding: 0px 20px;
}

.header {
  background: #566AB0;
}

.header__container {
  height: 90px;
  display: flex;
  align-items: center;
}

.header__logo {
  font-family: "Roboto", sans-serif;
  color: #fff;
  font-size: 22px;
  font-weight: 500;
}

.main {
  flex: 1 1 auto;
}

.footer {
  background: #566AB0;
}

.footer__container {
  height: 120px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.footer__creator {
  font-size: 16px;
  color: #fff;
  font-family: "Roboto", sans-serif;
}

.shorten__title {
  color: #fff;
  font-size: 25px;
  font-weight: 700;
  font-family: "Roboto", sans-serif;
  margin-bottom: 10px;
}

.shorten__search-input {
  width: 70%;
  background: linear-gradient(180deg, #FFFFFF 65.62%, rgba(211, 211, 211, 0.61) 100%);
  border-radius: 11px;
  height: 35px;
  padding: 20px;
  font-family: "Roboto", sans-serif;
}

.shorten__search-button {
  margin-left: 20px;
  color: white;
  font-family: "Roboto", sans-serif;
  font-size: 20px;
  background: #566AB0;
  height: 35px;
  padding: 0 20px;
  border-radius: 10px;
}

.shorten__search {
  margin-bottom: 10px;
}

.shorten__subtitle {
  color: #fff;
  font-size: 18px;
  font-family: "Roboto", sans-serif;
}

.shorten {
  margin-top: 40px;
}

.main {
  background: #222222;
}

.advantages {
  margin: 60px 0px;
}

.advantages__container {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
}

.advantages__item {
  flex: 0 0 33.3333%;
  margin: 0 50px 50px 50px;
}

.advantages__item-subtitle {
  text-align: center;
  color: #fff;
  font-size: 16px;
  text-transform: uppercase;
  font-family: "Roboto", sans-serif;
}

.advantages__item-title {
  text-align: center;
  color: #fff;
  font-size: 16px;
  text-transform: uppercase;
  font-family: "Roboto", sans-serif;
}

.advantages__item-img img {
  margin: 0 auto;
  display: block;
}

.shorten__result-link {
  color: purple;
  font-size: 18px;
  font-family: "Roboto", sans-serif;
}

@media (max-width: 641px) {
  .advantages__container {
    display: block;
    margin: 0;
  }
}

@media (max-width:590px) {
  .footer__container{
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }
  .footer__creator{
    margin-bottom: 10px;
  }
  .footer__creator:first-child{
    margin-top: 10px;
  }
}

@media (max-width: 429px) {
  .shorten__search {
    display: flex;
    flex-direction: column;
  }

  .shorten__search-button {
    margin: 20px 0 0 0;
  }

  .shorten__search-input {
    width: 100%;
  }
}
</style>
