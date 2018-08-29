<template>
  <div>
    <div class="row">
      <div class="col-md-12">
        <vuestic-widget :headerText="'Situação dos casos no ' + this.$store.state.app.dengueData.estado">
          <vuestic-data-table
          :apiMode="apiMode"
          :tableData="this.$store.state.app.tableData"
          :tableFields="tableFieldsCasos"
          :itemsPerPage="itemsPerPage"
          :sortFunctions="sortFunctions"
          :dataModeFilterableFields="dataModeFilterableFields"
          />

          <spring-spinner
            slot="loading"
            :animation-duration="2500"
            :size="70"
            color="#4ae387"
          />
        </vuestic-widget>
      </div>
    </div>

    <div class="row">
      <div class="col-md-12">
        <vuestic-widget :headerText="$t('tables.basic') + ' no ' + this.$store.state.app.dengueData.estado + ' em ' + this.$store.state.app.dengueData.ano ">
          <vuestic-data-table
          :apiMode="apiMode"
          :tableData="this.$store.state.app.tableData"
          :tableFields="tableFields"
          :itemsPerPage="itemsPerPage"
          :sortFunctions="sortFunctions"
          :dataModeFilterableFields="dataModeFilterableFields"
          />

          <spring-spinner
            slot="loading"
            :animation-duration="2500"
            :size="70"
            color="#4ae387"
          />
        </vuestic-widget>
      </div>
    </div>

  </div>
</template>

<script>

  import Vue from 'vue'
  import BadgeColumn from './BadgeColumn.vue'


  Vue.component('badge-column', BadgeColumn)

  export default {
    name: 'Table',

    data () {
      return {
        apiMode: false, // Choose api mode or just pass array in data-table component
        tableFields: [
          // {
          //   name: '__component:badge-column',
          //   title: 'Situação',
          //   dataClass: 'text-center'
          // },
          {
            title: 'Cidade',
            name: 'nome', // Object property name in your data e.g. (data[0].name)
            sortField: 'nome' // Object property name in your data which will be used for sorting
          },
          {
            title: 'Casos 2017',
            name: 'casos.f2017', // Object property name in your data e.g. (data[0].name)
          },
          {
            title: 'População 2017',
            name: 'populacao2017',
            sortField: 'populacao2017'
          },
          {
            title: '%',
            name: 'casos.p2017',
          }
        ],
        tableFieldsCasos: [
          // {
          //   name: 'cas',
          //   title: 'Situação',
          //   dataClass: 'table-info'
          // },
          {
            title: 'Cidade',
            name: 'nome', // Object property name in your data e.g. (data[0].name)
            sortField: 'nome' // Object property name in your data which will be used for sorting
          },
          {
            title: 'Casos',
            name: 'casos.f2013', // Object property name in your data e.g. (data[0].name)
            dataClass: 'text-center'
          },
          {
            title: '2013',
            name: 'casos.i2013', // Object property name in your data e.g. (data[0].name)
          },
          {
            title: 'Casos',
            name: 'casos.f2014', // Object property name in your data e.g. (data[0].name)
            dataClass: 'text-center'
          },
          {
            title: '2014',
            name: 'casos.i2014', // Object property name in your data e.g. (data[0].name)
          },
          {
            title: 'Casos',
            name: 'casos.f2015', // Object property name in your data e.g. (data[0].name)
            dataClass: 'text-center'
          },
          {
            title: '2015',
            name: 'casos.i2015', // Object property name in your data e.g. (data[0].name)
          },
          {
            title: 'Casos',
            name: 'casos.f2016', // Object property name in your data e.g. (data[0].name)
            dataClass: 'text-center'
          },
          {
            title: '2016',
            name: 'casos.i2016', // Object property name in your data e.g. (data[0].name)
          },
          {
            title: 'Casos',
            name: 'casos.f2017', // Object property name in your data e.g. (data[0].name)
            dataClass: 'text-center'
          },
          {
            title: '2017',
            name: 'casos.i2017', // Object property name in your data e.g. (data[0].name)
          }
          // {
          //   title: '%',
          //   name: 'crescimento',
          // }
        ],
        itemsPerPage: [  // values in dropdown "Items Per Page"
          {
            value: 10
          },
          {
            value: 20
          },
          {
            value: 50
          }
        ],
        sortFunctions: {       // use custom sorting functions for prefered fields
          'name': function (item1, item2) {
            return item1 >= item2 ? 1 : -1
          },
          'populacao2017': function (item1, item2) {
            return item1 >= item2 ? 1 : -1
          }
        },
        dataClass: {
          'nada': function () {
            return 'table-success'
          }
        },
        dataModeFilterableFields: ['nome', 'populacao2017'],
        // tableData: {},
        dengueData: {},
        // url: 'https://info.dengue.mat.br/api/alertcity?disease=dengue&format=jsonv&ew_start=1&ew_end=50',
        // requestData: {}
      }
    },
    mounted () {
      // EventBus.$on('getDengueData', data => {
      //   this.$nextTick(function () {
      //     this.dengueData = Object.assign({}, this.dengueData, data)
      //     switch (this.dengueData.id) {
      //       case 23: this.tableData = Object.assign({}, this.tableData, municipios23); break
      //       case 31: this.tableData = Object.assign({}, this.tableData, municipios31); break
      //       case 32: this.tableData = Object.assign({}, this.tableData, municipios32); break
      //       case 33: this.tableData = Object.assign({}, this.tableData, municipios33); break
      //       default: this.tableData = Object.assign({}, this.tableData, municipios41)
      //     }
      //     this.tableData.data.map(function (item) {
      //       item['ano2017'] = 200
      //       item['populacao2017'] = populacao.municipios[0]['POPULAÇÃO ESTIMADA']
      //       // let p = populacao.municipios.filter((populacao) => {
      //       //     return populacao.municipios.size === "small"
      //       // })
      //     })
      //   })
      // })

    }
  }
</script>

<style lang="scss">

  .color-icon-label-table {
    td:first-child {
      width: 1rem;
    }
  }
</style>
