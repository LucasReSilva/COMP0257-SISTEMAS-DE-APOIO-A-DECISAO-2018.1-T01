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
              <button @click="clickMe" class="btn btn-primary btn-micro"> Update </button>
            </div>
        </vuestic-widget>
      </div>
    </div>
  </div>
</template>

<script>
  // import { EventBus } from '../../event-bus.js'
  import ListaEstados from 'data/ListaEstados'
  import municipios23 from 'data/municipios23'
  import municipios31 from 'data/municipios31'
  import municipios32 from 'data/municipios32'
  import municipios33 from 'data/municipios33'
  import municipios41 from 'data/municipios41'
  import populacao from 'data/PopulacaoMunicipal'

  export default {
    name: 'dengue-form',
    computed: {
    },
    data () {
      return {
        dengueData: {},
        requestData: {},
        tableData: {},
        url: 'https://info.dengue.mat.br/api/alertcity?disease=dengue&format=json&ew_start=1&ew_end=50',
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
        anoSelectModel: {
          id: 7,
          ano: '2017',
        },
        estadoSelectModel: {
          id: 23,
          sigla: 'CE',
          nome: 'Ceará',
          regiao: {
            id: 2,
            sigla: 'NE',
            nome: 'Nordeste'
          }
        }
      }
    },
    methods: {
      clear (field) {
        this[field] = ''
      },
      clickMe () {
        this.dengueData = {
          ano: this.anoSelectModel.ano,
          estado: this.estadoSelectModel.nome,
          id: this.estadoSelectModel.id,
          sigla: this.estadoSelectModel.sigla
        }
        // EventBus.$emit('getDengueData', this.dengueData)

        // let cod = 3304557
        //
  
        // this.dengueData = Object.assign({}, this.dengueData, data)   ****REMOVER
        switch (this.dengueData.id) {
          case 23: this.tableData = Object.assign({}, this.tableData, municipios23); break
          case 31: this.tableData = Object.assign({}, this.tableData, municipios31); break
          case 32: this.tableData = Object.assign({}, this.tableData, municipios32); break
          case 33: this.tableData = Object.assign({}, this.tableData, municipios33); break
          default: this.tableData = Object.assign({}, this.tableData, municipios41)
        }
        // this.tableData.data.map(function (item) {
        var arrayLengthData = this.tableData.data.length
        for (var m = 0; m < arrayLengthData; m++) {
          let item = this.tableData.data[m]
          this.$http.get(this.url, {params: {ey_end: this.dengueData.ano,
            ey_start: this.dengueData.ano,
            geocode: item['id'] }}).then(result => {
              this.requestData = result.body
            }, error => {
              console.error(error)
            })

          let cod = Number(String(item['id']).substr(0, 2))
          // let t = populacao.municipios.find(p => (cod * 10 ** 5 + Number(p['COD. MUNIC'])) === item['id'])
          var arrayLength = populacao.municipios.length
          for (var i = 0; i < arrayLength; i++) {
            if ((cod * 10 ** 5 + Number(populacao.municipios[i]['COD. MUNIC'])) === item['id']) {
              item['populacao2017'] = populacao.municipios[i]['COD. MUNIC']
            }
          }
          let total = 0
          var arrayLengthCasos = this.requestData.length
          for (var c = 0; c < arrayLengthCasos; c++) {
            total += this.requestData[c]['casos']
            // console.log(this.requestData[c]['casos'])
          }
          item['casos2017'] = total
          console.log('id: ' + item['id'] + '**** total:' + total)
          console.log(item)
        }
        // })
      }
    },
    created () {
      this.$nextTick(() => {
        this.$validator.validateAll()
      })
      this.clickMe()
    },
    destroyed: function () {
      this.clickMe()
    }
  }
</script>

<style lang="scss">
  input[type=checkbox]:disabled + label, input[type=radio]:disabled + label,
  input[type=checkbox]:disabled, input[type=radio]:disabled {
    cursor: not-allowed;
  }
</style>
