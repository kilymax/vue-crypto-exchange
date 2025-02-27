<script>
export default {
  props: {
    convert: {
      type: Function,
      required: true,
    }
  }
}
</script>

<template>
  <div class="convertation">
    <input min="0" type="number" @input="convert($event.target.value)" placeholder="0">
  </div>
</template>

<style scoped lang="scss">
.convertation {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}
input {
  margin-block: 20px;
  border-radius: 3px;
  border: 0;
  padding: 10px 15px;
  background-color: white;
  color: rgb(49, 49, 49);
  outline: none;
  width: 500px;
  font-size: 1.5em;
}

</style>
