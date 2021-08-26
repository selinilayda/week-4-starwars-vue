<script>
export default {
  props: ['item'],
}
</script>
<template lang="pug">
NuxtLink.card(:to="`/starship/${item.name}`")
  img(src="@/assets/images/default.png")
  .description
    .key Name: 
    .value
      span {{ item.name }}   
  .description
    .key Model: 
    .value
      span {{ item.model }}
  .description
    .key HyperDrive Rating: 
    .value 
      i.fas.fa-star(v-for="i in parseInt(item.hyperdrive_rating)")
      i.far.fa-star(v-for="k in (5 - parseInt(item.hyperdrive_rating))")
  slot
  
  
</template>

<style lang="scss">
.card {
  border: 1px solid silver;
  text-align: center;
  text-decoration: none;
  color: white;
  img {
    height: 300px;
    width: 300px;
    object-fit: contain;
    transition: all 1s;
    &:hover {
      transform: scale(1.5);
    }
  }
  .description {
    display: flex;
    justify-content: space-between;
    padding: 10px;
    font-size: 18px;

    .value {
      font-weight: bold;
      i {
        color: yellow;
      }
    }
  }
}
</style>
