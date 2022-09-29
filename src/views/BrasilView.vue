<template>
  <div class="home">
    <BrazilStates/>
  </div>
</template>

<script>
// @ is an alias to /src
import BrazilStates from '@/components/maps/brazil/index.vue'

export default {
  name: 'HomeView',
  components: {
    BrazilStates
  }
}
</script>
