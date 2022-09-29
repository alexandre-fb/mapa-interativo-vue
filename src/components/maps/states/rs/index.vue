<template>
  <div class="container">
    <div @click="emitData" style="width: 100%;">
      <RSCitiesSvg />
    </div>
  </div>
</template>

<script>

import RSCitiesSvg from './svg-component.vue'
import citiesData from './citiesData'

export default {
  name: 'RSMap',
  components: {
    RSCitiesSvg
  },
  data(){
    return {
      cities: [],
      selectedCity: {},
      isHover: false,
    }
  },
  mounted() {
      this.cities = document.querySelectorAll('path')
      
      this.cities.forEach(city => {
        
        city.addEventListener('click', this.handleClick)
        city.addEventListener('mousemove', this.handleMouseMove)
        city.addEventListener('mouseleave', this.handleMouseLeave)
  
        const citySvgName = city.attributes.title.value
  
        citiesData.forEach(cityData => {
          if (cityData.pupulacao === 1 && citySvgName == cityData.nome.toUpperCase()) {
            city.style.fill = '#6cb859'
          }
          if (cityData.pupulacao === 2 && citySvgName == cityData.nome.toUpperCase()) {
            city.style.fill = '#cc00a3'
          }
          if (cityData.pupulacao === 3 && citySvgName == cityData.nome.toUpperCase()) {
            city.style.fill = '#eb732c'
          }
          if (cityData.pupulacao === 0 && citySvgName == cityData.nome.toUpperCase()) {
            city.style.fill = '#2cb8eb'
          }
        })
      })  
    },
  methods: {
    emitData() {
      const cityData = {
        selectedCity: this.selectedCity,
        isHover: this.isHover 
      }
      this.$emit('selectCity', cityData)
    },
    handleClick() {
      this.emitData()
    },
    handleMouseLeave() {
      this.isHover = false
      this.selectedCity = {}
      this.emitData()
    },
    handleMouseMove(event) {
      this.isHover = false

      for (let cityData of citiesData) {
        if(cityData.nome.toUpperCase() == event.target.attributes.title.value) {
          this.selectedCity = cityData
          this.isHover = true
          this.emitData()
        } 
      }
    }
  }
}
</script>

<style src='./style.scss' lang='scss' scoped></style>