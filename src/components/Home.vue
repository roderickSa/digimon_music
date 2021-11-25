<template>
  <div class="header" id="header">
    <div class="box-container music-container">
      <div class="music-description">
        <p>{{ current_digimon.music }}</p>
      </div>
      <div class="music-navigation">
        <audio 
          src="music/aim_sun_goes_down.mp3" 
          ref="audio"
          id="audio"></audio>
        <button id="prev" class="action-btn">
          <i class="fas fa-backward"></i>
        </button>
        <button 
          v-if="!is_paused"
          ref="play" 
          @click="play_music"
          id="play" 
          class="action-btn">
            <i class="fas fa-play"></i>
        </button>
        <button 
          v-else
          ref="pause" 
          @click="pause_music"
          id="pause" 
          class="action-btn">
            <i class="fas fa-pause"></i>
        </button>
        <button id="next" class="action-btn">
          <i class="fas fa-forward"></i>
        </button>
      </div>
      <div class="music-image">
        <p>progreso</p>
      </div>
    </div>
    <div class="box-container">
      <div class="carrusel-digimon">
        <div v-for="digimon in digimons" :key="digimon.id" class="box" @click="change_music(digimon)" >
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
      is_paused: false,
      current_digimon: {},
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
      this.change_music(data[0])
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    async play_music() {
      // console.log(this.$refs.audio.play());
      // document.getElementById("audio").play();
      this.$refs.audio.play()
      this.is_paused = true
    },
    async pause_music() {
      this.$refs.audio.pause()
      this.is_paused = false
    },
    change_music( { id, name, music } ) {
      const current_music = this.$refs.audio.src.substring(this.$refs.audio.src.lastIndexOf('/') + 1);
      //si la musica esta pausada
      if( this.is_paused == false ) {
        this.current_digimon = {
          id, name, music
        }
        // si es otra musica reiniciamos la musica
        if( music != current_music ) {
          const new_music = `music/${music}`
          this.$refs.audio.src = new_music
        }
        // si es la misma musica solo retomamos
        this.play_music()
        return
      }
      //si la musica NO esta pausada
      //si es otra musica
      if( music != current_music ) {
        const new_music = `music/${music}`
        this.$refs.audio.src = new_music
        this.play_music()
        this.current_digimon = {
          id, name, music
        }
      }
      //si la musica NO esta pausada
      //si es la misma musica => no hacemos nada
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
