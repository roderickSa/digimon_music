<template>
  <div 
    class="box"
    :class="{ 'selected_digimon': is_digimon_selected }" 
    ref="box"
    >
      <img :src="digimon.img" :alt="digimon.img">
      <div class="box-description">
        <p>{{digimon.music}}</p>
      </div>
  </div>
</template>

<script>
export default {
  name: 'DigimonItem',
  props: ['digimon', 'current_digimon'],
  data() {
    return {
    }
  },
  mounted(){
    this.observer = new MutationObserver(mutations => {
      //recorrea todos los elementos observados
      for (const m of mutations) {
        const newValue = m.target.getAttribute(m.attributeName);
        //this.$nextTick espera a que el dom actualice para recien actuar
        this.$nextTick(() => {
          this.onClassChange(newValue, m.oldValue);
        });
      }
    });

    //observara las clases de los refs(div box)
    this.observer.observe(this.$refs.box, {
      attributes: true,
      attributeOldValue : true,
      attributeFilter: ['class'],
    });
  },
  beforeUnmount() {
    this.observer.disconnect();
  }, 
  methods: {
    onClassChange(classAttrValue) {
      const arr_clases = classAttrValue.split(' ');
      if( arr_clases.includes('selected_digimon') ) {
        this.scrollToDigimonSelected()
      }
    },
    scrollToDigimonSelected() {
      if( document.querySelector('.box.selected_digimon') ) {
        document.querySelector('.box.selected_digimon').scrollIntoView({
            behavior: 'smooth', inline : 'center'
        })
      }
    }
  },
  computed: {
    is_digimon_selected() {
      return this.current_digimon.id === this.digimon.id
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
