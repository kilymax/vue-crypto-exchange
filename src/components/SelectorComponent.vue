<script>
export default {
  props: {
    setCrypto: {
      type: Function,
      required: true
    },
    cryptoCurrent: {
      type: String,
      required: true
    }
  },
}
</script>

<template>
  <ul>
    <li @click="setCrypto('BTC')" :className="cryptoCurrent == 'BTC' ? 'active' : ''">BTC</li>
    <li @click="setCrypto('ETH')" :className="cryptoCurrent == 'ETH' ? 'active' : ''">ETH</li>
    <li @click="setCrypto('USDT')" :className="cryptoCurrent == 'USDT' ? 'active' : ''">USDT</li>
    <li @click="setCrypto('SOL')" :className="cryptoCurrent == 'SOL' ? 'active' : ''">SOL</li>
  </ul>
</template>

<style scoped>
ul {
  list-style: none;
  padding: 0;
  border-radius: 3px;
  border: 3px solid black;
}

li {
  display: block;
  background: rgb(23, 23, 23);
  color: white;
  padding: 20px 0;
}

li:hover, li.active {
  background: rgb(10, 0, 64);
  cursor: pointer;
}
</style>
