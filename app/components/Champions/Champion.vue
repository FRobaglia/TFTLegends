<template>
<div>
<Header> </Header>
<div v-if="champion" class="champion-full">
  
  <div class="informations">

    <div class="idendity">
      <img class="champion-image" :src="`${image[champion.key + '_0']}`" :alt="champion.name">
      <h2> {{ champion.name }} </h2>
    </div>

    <ul class="classes">
      <li v-for="origin in champion.origin" :key="origin"> {{ origin }} </li>
      <li v-for="championClass in champion.class" :key="championClass"> {{ championClass }} </li>
    </ul>
  </div>

  <div class="ability">

      <h3 class="ability-title"> {{ champion.ability.name }} </h3>
      <p class="first-paragraph"> {{ champion.ability.description }} </p>

      <ul class="stats">
        <li v-for="stat in champion.ability.stats" :key="stat.type"> {{ stat.type }} : {{ stat.value }} </li>
      </ul>

  </div>

</div>
</div>
</template>


<script>
import image from '../../assets/img/champions/tiles/*.jpg'
import Header from '../Header'

export default {
  data() {
    return {
      champion: null,
      image: image
    };
  },
  mounted() {
    this.axios.get('https://solomid-resources.s3.amazonaws.com/blitz/tft/data/champions.json').then((response) => {
      const champions = response.data
      let result = [];
      for(var i in champions) {
        const champion = champions[i];
          result.push(champion);
      }
      result.forEach(champion => {
        if (champion.key === this.$route.params.champion) {
          this.champion = champion;
        }
      })
    })
  
  },
  components: {
    Header
  }
};
</script>