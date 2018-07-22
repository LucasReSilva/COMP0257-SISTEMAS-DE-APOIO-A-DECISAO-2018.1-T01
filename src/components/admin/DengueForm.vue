<template>
  <div class="form-elements">
    <div class="row">
      <div class="col-md-12">
        <vuestic-widget>
          <form>
            <div class="row">
              <fieldset>
                <vuestic-simple-select
                  :label="'forms.selects.simple' | translate"
                  v-model="simpleSelectModel"
                  option-key="description"
                  v-bind:options="simpleOptions">
                </vuestic-simple-select>
              </fieldset>
            </div>
            <div class="row" style="margin-bottom:50px;content: ''; clear: both; display: table;overflow: visible; z-index: 999;   position absolute; height: 120px;">
              <fieldset>
                <vuestic-multi-select
                  :label="'forms.selects.countryMulti' | translate"
                  v-model="multiSelectCountriesModel"
                  option-key="nome"
                  option-value="id"
                  v-bind:options="listaEstados">
                </vuestic-multi-select>
              </fieldset>
            </div>
          </form>
        </vuestic-widget>

      </div>
    </div>
  </div>
</template>

<script>
  import CountriesList from 'data/CountriesList'
  import ListaEstados from 'data/ListaEstados'

  export default {
    name: 'dengue-form',
    computed: {
    },
    data () {
      return {
        countriesList: CountriesList,
        listaEstados: ListaEstados,
        chosenCountry: '',
        simpleOptions: [
          {
            id: 1,
            description: '2011',
          },
          {
            id: 2,
            description: '2012',
          },
          {
            id: 3,
            description: '2013',
          },
          {
            id: 4,
            description: '2014',
          },
          {
            id: 5,
            description: '2015',
          },
          {
            id: 6,
            description: '2016',
          },
          {
            id: 7,
            description: '2017',
          },
        ],
        simpleSelectModel: '',
        multiSelectModel: [],
        multiSelectCountriesModel: [],
        multiSelectEstadosModel: [],

      }
    },
    methods: {
      clear (field) {
        this[field] = ''
      },
    },
    created () {
      this.$nextTick(() => {
        this.$validator.validateAll()
      })
    },
  }
</script>

<style lang="scss">
  input[type=checkbox]:disabled + label, input[type=radio]:disabled + label,
  input[type=checkbox]:disabled, input[type=radio]:disabled {
    cursor: not-allowed;
  }
</style>
