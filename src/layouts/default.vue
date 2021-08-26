<script>
import Header from '../components/Header.vue'
export default {
  name: 'DefaultLayout',
  components: {
    Header,
  },
}
</script>

<template lang="pug">
#starwars 
    Header
    Nuxt.content
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300&display=swap');
body {
  background: black;
  color: white;
  font-family: 'Poppins';

  .content {
    padding: 0 40px;
  }
}
</style>
