<template>
  <div>
    <div class="row">
      <div class="col-md-12">
        <vuestic-widget :headerText="$t('tables.styled')">
          <div class="table-responsive">
            <table class="table table-striped table-sm color-icon-label-table">
              <thead>
              <tr>
                <td>{{'tables.headings.status' | translate}}</td>
                <td>{{'tables.headings.city' | translate}}</td>
                <td align="right">Total {{'tables.headings.score' | translate}}</td>
              </tr>
              </thead>
              <tbody>
              <tr>
                <td></td>
                <td>Vancouver</td>
                <td align="right">93</td>
                <td align="middle"></td>
              </tr>
              <tr>
                <td></td>
                <td>Washington</td>
                <td align="right">280</td>
                <td align="middle"></td>
              </tr>
              <tr>
                <td></td>
                <td>Barcelona</td>
                <td align="right">16</td>
                <td align="middle"></td>
              </tr>
              <tr class="table-danger">
                <td>
                  <span class="badge badge-pill badge-danger">DANGER</span>
                </td>
                <td>Manchester</td>
                <td align="right">57</td>
                <td align="middle">
                  <i class="fa fa-exclamation-triangle icon-right input-icon error-icon"></i>
                </td>
              </tr>
              <tr class="table-success">
                <td>
                  <span class="badge badge-pill badge-primary">SUCCESS</span>
                </td>
                <td>Wien</td>
                <td align="right">113</td>
                <td align="middle" class="valid">
                  <i class="fa fa-check success-icon icon-right input-icon"></i>
                </td>
              </tr>
              <tr class="table-warning">
                <td>
                  <span class="badge badge-pill badge-warning">WARNING</span>
                </td>
                <td>Brussels</td>
                <td align="right">68</td>
                <td align="middle"></td>
              </tr>
              <tr>
                <td></td>
                <td>Vancouver</td>
                <td align="right">93</td>
                <td align="middle"></td>
              </tr>
              <tr class="table-info">
                <td>
                  <span class="badge badge-pill badge-info">INFO</span>
                </td>
                <td>Washington</td>
                <td align="right">280</td>
                <td align="middle"></td>
              </tr>
              </tbody>
            </table>
          </div>
        </vuestic-widget>
      </div>
    </div>

    <div class="row">
      <div class="col-md-12">
        <vuestic-widget :headerText="$t('tables.basic') + ' no ' + dengueData.estado + ' em ' + dengueData.ano ">
          <vuestic-data-table
          :apiMode="apiMode"
          :tableData="tableData"
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
  import { EventBus } from '../../event-bus.js'
  import municipios23 from 'data/municipios23'
  import municipios31 from 'data/municipios31'
  import municipios32 from 'data/municipios32'
  import municipios33 from 'data/municipios33'
  import municipios41 from 'data/municipios41'
  import populacao from 'data/PopulacaoMunicipal'
  // import TableData from 'data/TableData'


  Vue.component('badge-column', BadgeColumn)

  export default {
    name: 'Table',

    data () {
      return {
        apiMode: false, // Choose api mode or just pass array in data-table component
        tableFields: [
          {
            name: '__component:badge-column',
            title: 'Situação',
            dataClass: 'text-center'
          },
          {
            title: 'Cidade',
            name: 'nome', // Object property name in your data e.g. (data[0].name)
            sortField: 'nome' // Object property name in your data which will be used for sorting
          },
          {
            title: '2017',
            name: 'ano2017', // Object property name in your data e.g. (data[0].name)
          },
          {
            title: 'Populacao',
            name: 'populacao2017'
          }
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
          }
        },
        dataModeFilterableFields: ['nome'],
        tableData: {},
        dengueData: {}
      }
    },
    mounted () {
      EventBus.$on('getDengueData', data => {
        this.$nextTick(function () {
          this.dengueData = Object.assign({}, this.dengueData, data)
          switch (this.dengueData.id) {
            case 23: this.tableData = Object.assign({}, this.tableData, municipios23); break
            case 31: this.tableData = Object.assign({}, this.tableData, municipios31); break
            case 32: this.tableData = Object.assign({}, this.tableData, municipios32); break
            case 33: this.tableData = Object.assign({}, this.tableData, municipios33); break
            default: this.tableData = Object.assign({}, this.tableData, municipios41)
          }
          this.tableData.data.map(function (item) {
            item['ano2017'] = 200
            item['populacao2017'] = populacao.municipios[0]['POPULAÇÃO ESTIMADA']
            // let p = populacao.municipios.filter((populacao) => {
            //     return populacao.municipios.size === "small"
            // })
          })
        })
      })
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
