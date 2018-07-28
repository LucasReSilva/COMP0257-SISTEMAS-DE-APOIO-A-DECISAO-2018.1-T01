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
                  v-model="anoSelectModel"
                  option-key="ano"
                  v-bind:options="anosOptions">
                </vuestic-simple-select>
              </fieldset>
            </div>
            <div class="row" style="margin-bottom:50px;content: ''; clear: both; display: table;overflow: visible; z-index: 999;   position absolute; height: 120px;">
              <fieldset>
                <vuestic-simple-select
                  :label="'forms.selects.countryMulti' | translate"
                  v-model="estadoSelectModel"
                  option-key="nome"
                  option-value="id"
                  v-bind:options="listaEstados">
                </vuestic-simple-select>
              </fieldset>
            </div>
          </form>
            <div class="col-sm-6 d-flex justify-content-center align-items-center col-lg-12">
              <button @click="clickMe()" class="btn btn-primary btn-micro"> Update </button>
            </div>
        </vuestic-widget>
      </div>
    </div>
  </div>
</template>

<script>
  import ListaEstados from 'data/ListaEstados'
  import { EventBus } from '../../event-bus.js'

  export default {
    name: 'dengue-form',
    computed: {
    },
    data () {
      return {
        listaEstados: ListaEstados,
        anosOptions: [
          {
            id: 1,
            ano: '2011',
          },
          {
            id: 2,
            ano: '2012',
          },
          {
            id: 3,
            ano: '2013',
          },
          {
            id: 4,
            ano: '2014',
          },
          {
            id: 5,
            ano: '2015',
          },
          {
            id: 6,
            ano: '2016',
          },
          {
            id: 7,
            ano: '2017',
          },
        ],
        anoSelectModel: '',
        estadoSelectModel: ''
      }
    },
    methods: {
      clear (field) {
        this[field] = ''
      },
      clickMe () {
        let anoEstado = {
          ano: this.anoSelectModel.ano,
          estado: this.estadoSelectModel.nome,
          id: this.estadoSelectModel.id,
          sigla: this.estadoSelectModel.sigla
        }
        EventBus.$emit('getDengueData', anoEstado)
      }
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
