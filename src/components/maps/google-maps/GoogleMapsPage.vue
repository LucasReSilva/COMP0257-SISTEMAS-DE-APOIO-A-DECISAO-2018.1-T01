<template>
  <div class="google-maps-page">
    <div class="row">
      <div class="col-md-12">
        <vuestic-widget class="widget-viewport-height" :headerText="'Mapa de calor do ' + this.$store.state.app.dengueData.estado + ' em ' + this.$store.state.app.dengueData.ano">
          <!-- <google-map></google-map> -->
          <vue-google-heatmap :points="points"
                      :lat="points[0]['lat']"
                      :lng="points[0]['lng']"
                      :initial-zoom="7" />
        </vuestic-widget>
      </div>
    </div>
  </div>
</template>

<script>
  import GoogleMap from './GoogleMap'

  export default {
    name: 'google-maps-page',
    components: {
      GoogleMap
    },
    data () {
      return {
        points: JSON.parse(JSON.stringify(this.$store.state.app.coordenadasAtual))
      }
    }
  }
</script>

<style lang="scss">

</style>
