<template>
  <div class="google-maps-page">
    <div class="row">
      <div class="col-md-12">
        <vuestic-widget class="widget-viewport-height" headerText="Google Maps">
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
        // points: JSON.parse(JSON.stringify(this.$store.state.app.coordenadasAtual))
        points: [
          {lat: -7.356977, lng: -39.047547},
{lat: -7.356977, lng: -39.047547},
{lat: -4.223138, lng: -38.705624},
{lat: -4.223138, lng: -38.705624},
{lat: -2.885311, lng: -40.118241},
{lat: -2.885311, lng: -40.118241},
{lat: -6.092762, lng: -39.455705},
{lat: -6.092762, lng: -39.455705},
{lat: -6.563298, lng: -40.12316},
{lat: -6.563298, lng: -40.12316},
{lat: -3.586984, lng: -40.544638},
{lat: -3.586984, lng: -40.544638},
{lat: -6.997498, lng: -39.745821},
{lat: -6.997498, lng: -39.745821},
{lat: -5.522082, lng: -38.272778},
{lat: -5.522082, lng: -38.272778},
{lat: -3.364878, lng: -39.828823},
{lat: -3.364878, lng: -39.828823},
{lat: -6.779688, lng: -39.982387},
{lat: -6.779688, lng: -39.982387},
{lat: -3.948019, lng: -39.430423},
{lat: -3.948019, lng: -39.430423},
{lat: -3.906195, lng: -38.389803},
{lat: -3.906195, lng: -38.389803},
{lat: -4.567066, lng: -37.772753},
{lat: -4.567066, lng: -37.772753},
{lat: -4.370394, lng: -38.809441},
{lat: -4.370394, lng: -38.809441},
{lat: -4.751938, lng: -40.831097},
{lat: -4.751938, lng: -40.831097},
{lat: -7.206184, lng: -40.137446},
{lat: -7.206184, lng: -40.137446},
{lat: -4.416931, lng: -39.047555},
{lat: -4.416931, lng: -39.047555}
        ]
      }
    }
  }
</script>

<style lang="scss">

</style>
