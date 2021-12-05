<template>
  <div class="digimon-crud" >
    <div class="box-image-digimon-selected">
        <img :src="current_digimon.img" :alt="current_digimon.img">
    </div>
    <div class="form-digimon-selected">
        <h3>Edita la musica del Digimon</h3>
        <div class="inputBox">
            <select name="cbo_change_music" v-model="id_music_selected" @change="change_selected_music" >
                <option v-for="music in musics" :value="music.id" :key="music.id" >{{ music.name }}</option>
            </select>
        </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Digimon-Crud',
  props: ['musics', 'current_digimon'],
  data() {
    return {
        id_music_selected: null
    }
  },
  created() {
    //   console.log(this.current_digimon, 'dc')
      this.id_music_selected = this.current_digimon.id_music
  },
  methods: {
      change_selected_music(event) {
        //   console.log(event.target.value)
          this.$emit('change-music-digimon', event.target.value);
      }
  },
  //escuchamos los cambios del prop current_digimon
  watch: {
      //newVal, oldVal
      current_digimon: function() {
          this.id_music_selected = this.current_digimon.id_music
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
