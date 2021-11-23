<template>
  <div class="header" id="header">
    <div class="box-container">
      <div class="carrusel-digimon">
        <div v-for="digimon in digimons" :key="digimon.id" class="box">
          <img :src="digimon.img" :alt="digimon.img">
          <div class="box-description">
            <p>{{digimon.music}}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      digimons: []
    }
  },
  props: {
    // msg: String
  },
  async created () {
    try {
      const response = await fetch(`http://127.0.0.1:8001/api/digimons`, {
          'method': 'POST'      
      });
      const data = await response.json();
      this.digimons = data;
    } catch (error) {
      console.log(error);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
