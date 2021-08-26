<script>
import Card from '../../components/Card.vue'

export default {
  components: {
    Card,
  },
  data() {
    return {
      card: null,
    }
  },
  async mounted() {
    const response = await this.getAllDataWhereByNameOrModel(
      this.$route.params.name
    )
    this.card = response.data.results[0] || null
  },
  methods: {
    async getAllDataWhereByNameOrModel(search) {
      return await this.$axios.get(
        `https://swapi.dev/api/starships?search=${search}`
      )
    },
  },
}
</script>

<template lang="pug">
#starships
  NuxtLink(to="/starship")
    button Back 
  Card.card(:item="card" v-if="card")
    .description
      .key Passengers: 
      .value
        span {{ card.passengers }}
    .description
      .key Max Atmosphering Speed: 
      .value
        span {{ card.max_atmosphering_speed }}
    .description
      .key Manufacture: 
      .value
        span {{ card.manufacturer }}
    .description
      .key Crew: 
      .value
        span {{ card.crew }}
    .description
      .key Cargo Capacity: 
      .value
        span {{ card.cargo_capacity }}
    
    
</template>

<style lang="scss" scoped>
#starships {
  width: 100%;
  text-align: left;

  button {
    border: none;
    background: yellow;
    color: black;
    font-size: 17px;
    font-weight: bold;
    padding: 10px 20px;
    border-radius: 15px;
  }

  .card {
    display: block;
    width: 600px;
    margin: auto;
    margin-top: 50px;
  }
}
</style>
