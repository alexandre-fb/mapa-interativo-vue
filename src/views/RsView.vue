<template>
  <div class="home">
    <RSCities/>
  </div>
</template>

<script>
// @ is an alias to /src
import RSCities from '@/components/maps/states/rs/index.vue'

export default {
  name: 'AboutView',
  components: {
    RSCities
  }
}
</script>