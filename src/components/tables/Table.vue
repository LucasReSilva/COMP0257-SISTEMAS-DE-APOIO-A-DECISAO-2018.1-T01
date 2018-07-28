<template>
  <div>
    <div class="row">
      <div class="col-xs-12 col-md-12">
        <vuestic-widget :headerText="$t('tables.basic')">
          <div class="table-responsive">
            <table class="table table-striped first-td-padding">
              <thead>
                {{ dengueData }}
              <tr>
                <td>#</td>
                <td>{{'tables.headings.city' | translate}}</td>              
                <td align="right">{{'tables.headings.score' | translate}}</td>
                <td></td>
              </tr>
              </thead>
              <tbody>
              <tr>
                <td>#</td>
                <td>Vancouver</td>
                <td align="right">93</td>
                <td></td>
              </tr>
              <tr>
                <td>#</td>
                <td>Washington</td>
                <td align="right">280</td>
                <td></td>
              </tr>
              <tr>
                <td>#</td>
                <td>Barcelona</td>
                <td align="right">16</td>
                <td></td>
              </tr>
              <tr>
                <td>#</td>
                <td>Manchester</td>
                <td align="right">57</td>
                <td></td>
              </tr>
              <tr>
                <td>#</td>
                <td>Wien</td>
                <td align="right">113</td>
                <td></td>
              </tr>
              <tr>
                <td>#</td>
                <td>Brussels</td>
                <td align="right">68</td>
                <td></td>
              </tr>
              </tbody>
            </table>
          </div>
        </vuestic-widget>
      </div>
    </div>

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

  </div>
</template>

<script>
  import Vue from 'vue'
  import BadgeColumn from './BadgeColumn.vue'
  import FieldsDef from 'vuestic-components/vuestic-datatable/data/fields-definition'
  import ItemsPerPageDef from 'vuestic-components/vuestic-datatable/data/items-per-page-definition'
  import QueryParams from 'vuestic-components/vuestic-datatable/data/query-params'
  import { EventBus } from '../../event-bus.js'


  Vue.component('badge-column', BadgeColumn)

  export default {
    name: 'Table',

    data () {
      return {
        apiUrl: 'https://vuetable.ratiw.net/api/users',
        apiMode: true,
        tableFields: FieldsDef.tableFields,
        itemsPerPage: ItemsPerPageDef.itemsPerPage,
        sortFunctions: FieldsDef.sortFunctions,
        paginationPath: '',
        defaultTablePerPage: 6,
        queryParams: QueryParams,
        dengueData: {}
      }
    },
    mounted () {
      EventBus.$on('getDengueData', data => {
        this.dengueData = data
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
