<template>
    <div class="container">
        <section class="maps__section">
            <div class="map__container">
                <transition name="fade">   
                    <div class="map__brazil " @click="handleBrazilMapClick" v-if="!showState">
                        <BrazilMap @selectState="setBrazilData" />
                    </div>
                </transition>
                    
                <span class="map__label" v-if="!showState">
                    {{selectedState.nome}}
                </span>
            </div>

            <div class="map__container">
                <transition name="show-state">    
                    <div class="map__rs" v-if="showState && selectedState.nome == 'Rio Grande do Sul'" @click="handleStateMapClick">
                        <RsMap @selectCity="setStateData" />
                    </div>
                </transition>
                
                <span class="map__label">
                    {{selectedCity.nome}}
                </span>
                
                <transition name="fade">
                    <button class="btn" v-if="showState" @click="handleBackBtnClick">
                        Voltar
                    </button>
                </transition>
            </div>
        </section>

        <section class="info__section">
             
                <transition name="fade">
                    <div v-if="showState">
                        <h1>{{dataToShow.nome}}</h1>
                        <p>{{dataToShow.descricao}}</p>
                    </div>
                </transition>
            
        </section>
  </div>
</template>

<script>
import BrazilMap from '../maps/brazil/index.vue'
import RsMap from '../maps/states/rs/index.vue'

export default {
  name: 'BrazilStates',
  components: {
    BrazilMap,
    RsMap
  },
  data(){
    return {
        showState: false,
        selectedState: {},
        selectedCity: {},
        dataToShow: {},
        isBrazilMapHover: false,
        isStateMapHover: false
    }
  },
  methods:{
    setBrazilData(selectedStateData) {
        this.selectedState = selectedStateData.selectedState
        this.isBrazilMapHover = selectedStateData.isHover
    },
    setStateData(selectedCityData) {
        this.selectedCity = selectedCityData.selectedCity
        this.isStateMapHover = selectedCityData.isHover
    },
    handleBrazilMapClick(){
        if (this.isBrazilMapHover) {
            this.showState = true
        }
        this.dataToShow = this.selectedState
    },
    handleStateMapClick(){
        this.dataToShow = this.selectedCity
    },
    handleBackBtnClick(){
        this.showState = false
        this.selectedState = {}
        this.selectedCity = {}
    },
  }
}
</script>
<style src='./style.scss' lang='scss' scoped></style>

