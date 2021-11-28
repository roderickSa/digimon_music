<template>
  <div>
    <Header
      :is_paused="is_paused"
      :current_digimon="current_digimon"
      :play_music="play_music"
      :pause_music="pause_music"
      :ended_music="ended_music"
      :timeupdate_music="timeupdate_music"
      :set_progress="set_progress"
      ref="header"/>
    <div class="box-container">
      <Digimon 
        :digimons="digimons" 
        :change_music="change_music" />
    </div>
  </div>
</template>

<script>

import Digimon from '@/components/Digimon';
import Header from '@/components/Header';

export default {
  name: 'Home',
  components: {
    Digimon,
    Header
  },
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
      // this.$refs.audio.play()
      this.$refs.header.$refs.audio.play()
      this.is_paused = true
    },
    async pause_music() {
      // this.$refs.audio.pause()
      this.$refs.header.$refs.audio.pause()
      this.is_paused = false
    },
    change_music( { id, name, music } ) {
      const audio = this.$refs.header.$refs.audio
      const current_music = audio.src.substring(audio.src.lastIndexOf('/') + 1);
      //si la musica esta pausada
      if( this.is_paused == false ) {
        this.current_digimon = {
          id, name, music
        }
        // si es otra musica reiniciamos la musica
        if( music != current_music ) {
          const new_music = `music/${music}`
          audio.src = new_music
        }
        // si es la misma musica solo retomamos
        this.play_music()
        return
      }
      //si la musica NO esta pausada
      //si es otra musica
      if( music != current_music ) {
        const new_music = `music/${music}`
        audio.src = new_music
        this.play_music()
        this.current_digimon = {
          id, name, music
        }
      }
      //si la musica NO esta pausada
      //si es la misma musica => no hacemos nada
    },
    ended_music() {
      const inx = this.digimons.findIndex( item => ( item.id === this.current_digimon.id ) )
      if( inx !== -1 ) {
        const new_digimon = this.tamanio_digimon - 1 !== inx? this.digimons[inx + 1]: this.digimons[0]
        return this.change_music(new_digimon)
      }
    },
    timeupdate_music() {
      const audio = this.$refs.header.$refs.audio
      const duration = audio.duration
      const currentTime = audio.currentTime
      const progressPercent = ( currentTime / duration ) * 100
      // console.log(progressPercent);
      document.getElementById("progress").style.width = `${progressPercent}%`
    },
    set_progress(e) {
      const audio = this.$refs.header.$refs.audio
      const content_progress = this.$refs.header.$refs.content_progress
      const duration = audio.duration
      const width = content_progress.clientWidth
      const new_posX = e.offsetX
      audio.currentTime = ( new_posX / width ) * duration
    }
  },
  computed: {
    tamanio_digimon() {
      return this.digimons.length
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
