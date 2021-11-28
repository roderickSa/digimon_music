<template>
    <div class="header box-container" id="header">
        <div class="music-container">
            <div class="music-description">
                <p>{{ current_digimon.music }}</p>
            </div>
        </div>
        <div class="music-navigation">
            <audio 
                src="music/aim_sun_goes_down.mp3" 
                ref="audio"
                id="audio"
                v-on:ended="my_ended_music"
                v-on:timeupdate="my_timeupdate_music"></audio>
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
            <div 
                class="content-progress"
                ref="content_progress"
                @click="my_set_progress($event)"
                >
                <div 
                    class="progress" 
                    id="progress"/>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Header',
  props:    ['is_paused', 'current_digimon', 'play_music', 'pause_music', 'ended_music', 'timeupdate_music', 'set_progress'],
  data() {
    return {
    }
  },
  methods: {
      my_play_music(digimon) {
          this.play_music(digimon);
      },
      my_ended_music(){
          this.ended_music()
      },
      my_timeupdate_music() {
          this.timeupdate_music()
      },
      my_set_progress(e) {
          this.set_progress(e)
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
