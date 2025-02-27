<script>
export default {
  props: {
    favs: {
      type: Array,
      required: true
    },
    getFromFavs: {
      type: Function,
      required: true
    }
  }
}
</script>

<template>
  <h2>Избранные пары:</h2>
  <div @click="getFromFavs(index)" v-for="(elem, index) in favs" :key="index">
    <span>{{ elem.from }}</span>
    <span>{{ elem.to }}</span>
  </div>
</template>

<style scoped lang="scss">
  div {
    display: flex;
    justify-content: space-between;
    width: 500px;
    transform: scale(0.95);
    margin: 10px auto;
    transition: all 0.5s ease;
    opacity: 0.7;

    &:hover {
      opacity: 1;
      transform: scale(1);
      cursor: pointer;
    }
  }

  span {
    padding: 10px 15px;
    background-color: rgb(55, 95, 255);
  }

</style>
