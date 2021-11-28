<template>
  <div>
      <img :src="digimon.img" :alt="digimon.img">
      <div class="box-description">
        <p>{{digimon.music}}</p>
      </div>
  </div>
</template>

<script>
export default {
  name: 'DigimonItem',
  props: ['digimon'],
  data() {
    return {
    }
  },
  created(){
    //   console.log(this.$attrs);
  },
  methods: {
    //   my_change_music(digimon) {
    //       this.change_music(digimon);
    //   }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
