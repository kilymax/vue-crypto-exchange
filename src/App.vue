<script>
import FavoriteComponent from './components/FavoriteComponent.vue';
import InputComponent from './components/InputComponent.vue';
import Selector from './components/SelectorComponent.vue';
import CryptoConvert from 'crypto-convert';

const convert = new CryptoConvert();

export default {
  components: {InputComponent, Selector, FavoriteComponent},
  data() {
    return {
      amount: 0,
      cryptoSell: '',
      cryptoBuy: '',
      error: '',
      result: 0,
      resultString: '',
      favs: []
    }
  },
  methods: {
    setCryptoSell(val) {
      this.cryptoSell = val
    },
    setCryptoBuy(val) {
      this.cryptoBuy = val
    },
    change() {
      if(this.result != 0) {
        alert("Вы успешно обменяли валюту!")
      }
    },
    getFromFavs(index) {
      this.cryptoSell = this.favs[index].from
      this.cryptoBuy = this.favs[index].to
    },
    addToFavorite() {
      this.favs.push({
        from: this.cryptoSell,
        to: this.cryptoBuy
      })
    },
    async convert(val) {
      this.amount = val
      this.resultString = ''

      if(this.amount <= 0) {
        this.error = 'Число должно быть больше нуля'
        return
      } else if(this.cryptoSell == '' || this.cryptoBuy == '') {
        this.error = 'Выберите валюту'
        return
      } else if(this.cryptoSell == this.cryptoBuy) {
        this.error = 'Валюты не могут быть одинаковыми!'
        return
      }
      this.error = ''

      await convert.ready()
      this.result = convert[this.cryptoSell][this.cryptoBuy](this.amount)
      this.resultString = `${this.amount} ${this.cryptoSell} = ${this.result} ${this.cryptoBuy}`
    }
  }
}
</script>

<template>
  <h1>Crypto</h1>
  <div class="selectors">
    <Selector :setCrypto="setCryptoSell" :cryptoCurrent="cryptoSell"/>
    <Selector :setCrypto="setCryptoBuy" :cryptoCurrent="cryptoBuy"/>
  </div>
  <button @click="addToFavorite()">В избранное</button>
  <FavoriteComponent :favs="favs" v-if="favs.length > 0" :getFromFavs="getFromFavs"/>

  <InputComponent :convert="convert"/>
  <p class="result">{{ resultString }}</p>
  <button @click="change()">Обменять</button>
  <p class="error" v-if="error != 0">{{ error }}</p>
</template>

<style scoped>
h1 {
  margin-block: 50px;
}
.selectors {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
  margin: auto;
}

.result {
  padding: 20px;
  min-height: 30px;
  font-size: 20px;
}

.error {
  color: red;
}

button {
  border-radius: 3px;
  border: 0;
  padding: 10px 15px;
  background-color: rgb(0, 94, 0);
  color: rgb(255, 255, 255);
  outline: none;
  font-size: 1.5em;

  &:hover {
    background-color: green;
  }
}

</style>
