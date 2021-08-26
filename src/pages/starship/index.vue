<script>
// import Card from '../components/Card'

export default {
  name: 'Index',
  data() {
    return {
      data: [],
      loading: true,
      searchText: null,
    }
  },

  watch: {
    async searchText(value) {
      const response = await this.getAllDataWhereByNameOrModel(value)
      this.data = response.data.results || []
    },
  },

  async mounted() {
    try {
      this.loading = true
      const response = await this.getAllData()
      this.data = response.data.results
    } catch (error) {
    } finally {
      this.loading = false
    }
  },

  methods: {
    async getAllData() {
      return await this.$axios.get('https://swapi.dev/api/starships/')
    },

    async getAllDataWhereByNameOrModel(search) {
      return await this.$axios.get(
        `https://swapi.dev/api/starships?search=${search}`
      )
    },
  },
}
</script>
<template lang="pug">
main
  .search-text-box
    input(type="text" placeholder="Enter a name or model" v-model="searchText")
  .cards(v-if="!loading")
    Card.card(v-for="(item,index) in data" :key="index" :item="item")
  .loading(v-else)
    img(src="@/assets/images/loading.gif")
  
  h3(v-if="!data.length && !loading") Sonuç bulunamadı.
</template>

<style lang="scss">
.search-text-box {
  text-align: center;
  margin-bottom: 40px;

  input {
    background: transparent;
    border: 1px solid silver;
    border-radius: 10px;
    padding: 15px 30px;
    font-size: 20px;
    color: white;
    // &:hover {
    //   border-radius: 10px;
    // }
    &:focus {
      outline-color: yellow;
    }
    // &:active {
    //   border-radius: 10px;
    //   outline: none;
    // }
  }
}

.loading {
  text-align: center;
}

h3 {
  text-align: center;
}

.cards {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;

  @media (max-width: 1024px) {
    grid-template-columns: repeat(3, 1fr);
  }
  @media (max-width: 890px) {
    grid-template-columns: repeat(2, 1fr);
  }
}
</style>
