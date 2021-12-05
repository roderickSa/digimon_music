<template>
  <div>
    <Header
      :is_paused="is_paused"
      :current_digimon="current_digimon"
      :play_music="play_music"
      :pause_music="pause_music"
      :next_music="next_music"
      :previ_music="previ_music"
      :ended_music="ended_music"
      :timeupdate_music="timeupdate_music"
      :set_progress="set_progress"
      ref="header"/>
    <div class="box-container">
      <Digimon 
        :digimons="digimons"
        :current_digimon="current_digimon"
        :change_music="change_music" />
    </div>
    <DigimonCrud
      :musics="musics"
      :current_digimon="current_digimon"
      @change-music-digimon="on_change_selected_music"
    />
  </div>
</template>

<script>

import Header from '@/components/Header';
import Digimon from '@/components/Digimon';
import DigimonCrud from '@/components/DigimonCrud';

export default {
  name: 'Home',
  components: {
    Digimon,
    Header,
    DigimonCrud
  },
  data() {
    return {
      is_paused: false,
      current_digimon: {},
      digimons: [],
      musics: []
    }
  },
  props: {
    // msg: String
  },
  async created () {
    try {
      //digimon
      const response = await fetch(`http://127.0.0.1:8001/api/digimons`, {
          'method': 'POST'      
      });
      const data = await response.json();
      this.digimons = data;
      this.change_music(data[0])
      //music
      const response_music = await fetch(`http://127.0.0.1:8001/api/musics`, {
          'method': 'POST'      
      });
      const data_music = await response_music.json();
      this.musics = data_music
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    async play_music() {
      // console.log(this.$refs.audio.play());
      // document.getElementById("audio").play();
      // this.$refs.audio.play()
      await this.$refs.header.$refs.audio.play()//aca importante el await por que el play es una promesa
      this.is_paused = true
    },
    async pause_music() {
      // this.$refs.audio.pause()
      await this.$refs.header.$refs.audio.pause()
      this.is_paused = false
    },
    async change_music( { id, name, img, music, id_music } ) {
      const audio = this.$refs.header.$refs.audio
      const current_music = audio.src.substring(audio.src.lastIndexOf('/') + 1);
      //si la musica esta pausada
      if( this.is_paused == false ) {
        this.current_digimon = {
          id, name, img, music, id_music
        }
        // si es otra musica reiniciamos la musica
        if( music != current_music ) {
          const new_music = `music/${music}`
          audio.src = new_music
        }
        // si es la misma musica solo retomamos
        await this.play_music()
        return
      }
      //si la musica NO esta pausada
      //si es otra musica
      if( music != current_music ) {
        const new_music = `music/${music}`
        audio.src = new_music
        await this.play_music()
        this.current_digimon = {
          id, name, img, music, id_music
        }
      }
      //si la musica NO esta pausada
      //si es la misma musica => no hacemos nada
    },
    async previ_music() {
      const inx = this.digimons.findIndex( item => ( item.id === this.current_digimon.id ) )
      if( inx !== -1 ) {
        const new_digimon = inx !== 0? this.digimons[inx - 1]: this.digimons[this.tamanio_digimon - 1]
        await this.change_music(new_digimon)
        return 
      }  
    },
    async next_music() {
      const inx = this.digimons.findIndex( item => ( item.id === this.current_digimon.id ) )
      if( inx !== -1 ) {
        const new_digimon = this.tamanio_digimon - 1 !== inx? this.digimons[inx + 1]: this.digimons[0]
        return await this.change_music(new_digimon)
      }
    },
    async ended_music() {
      await this.next_music()
      // const inx = this.digimons.findIndex( item => ( item.id === this.current_digimon.id ) )
      // if( inx !== -1 ) {
      //   const new_digimon = this.tamanio_digimon - 1 !== inx? this.digimons[inx + 1]: this.digimons[0]
      //   return this.change_music(new_digimon)
      // }
    },
    async timeupdate_music() {
      const audio = this.$refs.header.$refs.audio
      const duration = audio.duration
      const currentTime = audio.currentTime
      const progressPercent = ( currentTime / duration ) * 100
      // console.log(progressPercent);
      document.getElementById("progress").style.width = `${progressPercent}%`
    },
    async set_progress(e) {
      const audio = this.$refs.header.$refs.audio
      const content_progress = this.$refs.header.$refs.content_progress
      const duration = audio.duration
      const width = content_progress.clientWidth
      const new_posX = e.offsetX
      audio.currentTime = ( new_posX / width ) * duration
    },
    async on_change_selected_music(id_music) {
      const inx_music = this.musics.findIndex( m => (m.id === parseInt(id_music)) )
      // console.log(id_music)
      if( inx_music === -1 ) {
        return
      }
      // console.log("ce")
      const inx_digimon = this.digimons.findIndex( d => (d.id === this.current_digimon.id) )
      if( inx_digimon === -1 ) {
        return
      }
      // console.log("ca")
      const new_music = this.musics[inx_music]
      this.digimons[inx_digimon].id_music = new_music.id;
      this.digimons[inx_digimon].music = new_music.music;
      this.current_digimon = {...this.current_digimon, id_music: new_music.id, music: new_music.music}
      await this.pause_music()
      await this.change_music(this.digimons[inx_digimon])
      // await this.play_music()
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
