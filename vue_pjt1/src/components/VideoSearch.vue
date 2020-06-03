<template>
  <div class="">
    <input @keypress.enter="search" type="text" v-model="input">
    <button @click="search">search</button>
  </div>
</template>

<script>
export default {
  name: 'VideoSearch',
  data() {
    return {
      input: '',
    }
  },
  methods: {
    search() {
      this.$emit('search-list', this.input)
    }
  }
}
</script>

<style>

</style>