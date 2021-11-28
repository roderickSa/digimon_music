<template>
  <div class="carrusel-digimon" >
    <digimon-item 
      v-for="digimon in digimons" 
      :key="digimon.id" 
      :digimon="digimon"
      class="box" 
      @click="my_change_music(digimon)" />
  </div>
</template>

<script>

import DigimonItem from '@/components/DigimonItem';

export default {
  name: 'Digimon',
  components: {
      DigimonItem
  },
  props:    ['digimons', 'change_music'],
  data() {
    return {
    }
  },
  methods: {
      my_change_music(digimon) {
          this.change_music(digimon);
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
