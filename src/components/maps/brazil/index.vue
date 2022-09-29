<template>
  <div class="container">
    <div @click="emitData" style="width: 100%;">
      <BrazilStatesSvg />
    </div>
  </div>
</template>

<script>

import BrazilStatesSvg from './svg-component.vue'
import statesData from './statesData'

export default {
  name: 'BrazilMap',
  components: {
    BrazilStatesSvg
  },
  data(){
    return {
      states: [],
      selectedState: {},
      isHover: false,
    }
  },
  mounted() {
    this.states = document.getElementsByTagName('path')
      
    for (let state of this.states) {
      state.addEventListener('click', this.handleClick)
      state.addEventListener('mousemove', this.handleMouseMove)
      state.addEventListener('mouseleave', this.handleMouseLeave)
    }
  },
  methods: {
    emitData() { 
      const stateData = {
        selectedState: this.selectedState,
        isHover: this.isHover 
      }
      this.$emit('selectState', stateData)
    },
    handleClick(){
      this.emitData()
    },
    handleMouseLeave() {
      this.isHover = false
      this.selectedState = {}
      this.emitData()
    },
    handleMouseMove(event) {
      this.isHover = false
  
      for (let stateData of statesData) {
        if(stateData.nome == event.target.attributes.title.value) {
          this.selectedState = stateData
          this.isHover = true
          this.emitData()
        } 
      } 
    }
  }
}
</script>

<style src='./style.scss' lang='scss' scoped></style>