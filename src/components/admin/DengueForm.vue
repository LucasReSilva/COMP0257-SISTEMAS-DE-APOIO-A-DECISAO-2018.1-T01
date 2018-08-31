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
              <button @click="update" class="btn btn-primary btn-micro"> Update </button>
              <!-- <button @click="mudaNois" class="btn btn-primary btn-micro"> Muda </button> -->
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
  computed: {},
  data () {
    return {
      promesasEmVao: [],
      tableData: { data: [] },
      url:
        'https://info.dengue.mat.br/api/alertcity?disease=dengue&format=json&ew_start=1&ew_end=50',
      listaEstados: ListaEstados,
      anosOptions: [
        {
          id: 1,
          ano: '2013'
        },
        {
          id: 2,
          ano: '2014'
        },
        {
          id: 3,
          ano: '2015'
        },
        {
          id: 4,
          ano: '2016'
        },
        {
          id: 5,
          ano: '2017'
        }
      ],
      anoSelectModel: {
        id: 7,
        ano: '2017'
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
    update () {
      this.$store.commit('setLoading', true)
      let dengueData = {
        ano: this.anoSelectModel.ano,
        estado: this.estadoSelectModel.nome,
        id: this.estadoSelectModel.id,
        sigla: this.estadoSelectModel.sigla,
        lat: this.estadoSelectModel.lat,
        lng: this.estadoSelectModel.lng
      }
      this.$store.commit('setDengueData', dengueData)
      // this.$store.commit('resetCoordenadasAtual')

      if (this.$localStorage.get(dengueData.estado)) {
        this.$store.commit(
          'setTableData',
          JSON.parse(this.$localStorage.get(dengueData.estado))
        )
        this.$store.commit(
          'setCoordenadas',
          JSON.parse(this.$localStorage.get('coordenadasAtual'))
        )
      } else {
        this.tableData = { data: [] }
        switch (dengueData.id) {
          case 23:
            this.tableData = Object.assign({}, this.tableData, municipios23)
            break
          case 31:
            this.tableData = Object.assign({}, this.tableData, municipios31)
            break
          case 32:
            this.tableData = Object.assign({}, this.tableData, municipios32)
            break
          case 33:
            this.tableData = Object.assign({}, this.tableData, municipios33)
            break
          default:
            this.tableData = Object.assign({}, this.tableData, municipios41)
        }
        this.$store.commit('setTableData', this.tableData)
        var arrayLengthData = this.$store.state.app.tableData.data.length
        for (var m = 0; m < arrayLengthData; m++) {
          let item = this.$store.state.app.tableData.data[m] // alias para o item atual da tabela de dados
          let cod = Number(String(item['id']).substr(0, 2)) // codigo do estado
          var arrayLength = populacao.municipios.length
          for (var i = 0; i < arrayLength; i++) {
            if (
              cod * 10 ** 5 + Number(populacao.municipios[i]['COD. MUNIC']) ===
              item['id']
            ) {
              this.updateTableDataItem(
                m,
                'populacao2017',
                populacao.municipios[i]['POPULAÇÃO ESTIMADA']
              )
              let casos = this.seedCasos(
                populacao.municipios[i]['POPULAÇÃO ESTIMADA']
              )
              this.updateTableDataItem(m, 'casos', casos)
              this.updateCoordenadasAtual(
                populacao.municipios[i]['LATITUDE'],
                populacao.municipios[i]['LONGITUDE'],
                casos['f' + dengueData.ano]
              ) // casos['f' + dengueData.ano]
            }
          }
        }
      }
      this.$store.commit(
        'setDataTableCoordenadas',
        this.$store.state.app.coordenadasAtual
      )
      this.$store.commit('setLoading', false)
      this.$localStorage.set(
        dengueData.estado,
        JSON.stringify(this.$store.state.app.tableData)
      )
      this.$localStorage.set(
        'coordenadasAtual',
        JSON.stringify(this.$store.state.app.coordenadasAtual)
      )

      console.log('Dados Atualizados') // descolar um LADA
    },
    getCasosData (codigo) {
      let myPromise = new Promise((resolve, reject) => {
        let data
        data = this.$http.get(this.url, {
          params: {
            ey_end: this.$store.state.app.dengueData.ano,
            ey_start: this.$store.state.app.dengueData.ano,
            geocode: codigo
          }
        })
        resolve(data)
      })
      this.promesasEmVao.push(myPromise)
      // let total = 0
      // myPromise.then(data => {
      //   let arrayLengthCasos = data.length
      //   for (var c = 0; c < arrayLengthCasos; c++) {
      //     total += Number(data[c]['casos'])
      //       // console.log(this.requestData[c]['casos'])
      //   }
      // }).catch(() => {
      //   console.log('There was an error')
      // })
    },
    updateTableDataItem (itemIndex, field, value) {
      this.$store.commit('updateTableDataItem', {
        itemIndex: itemIndex,
        field: field,
        value: value
      })
    },
    updateCoordenadasAtual (lat, lng, qtd) {
      let coordenadas = []
      for (let index = 0; index < qtd; index++) {
        coordenadas.push({ lat: lat, lng: lng })
      }
      this.$store.commit('updateCoordenadasAtual', coordenadas)
      console.log(qtd)
    },
    seedCasos (populacao) {
      populacao = String(populacao)
      if (populacao.length <= 4) {
        populacao = '0' + populacao
      }
      let casoBase = Math.floor(Number(populacao) / 1000)
      // let fakeCasos = {}
      let fakeCasos = Object.assign(
        {},
        this.createCasoObject(2013, populacao, casoBase, 0),
        this.createCasoObject(2014, populacao, casoBase, 1),
        this.createCasoObject(2015, populacao, casoBase, 2),
        this.createCasoObject(2016, populacao, casoBase, 3),
        this.createCasoObject(2017, populacao, casoBase, 4)
      )
      return fakeCasos
    },
    createCasoObject (ano, populacao, casoBase, index) {
      let obj = {}
      obj['f' + ano] = Math.floor(
        (Number(populacao[index]) / 3 + 1) * casoBase
      )
      let indicador = obj['f' + ano] / Number(populacao) * 100000
      if (indicador < 100) {
        obj['i' + ano] = '✅'
      } else if ((indicador >= 100) & (indicador <= 300)) {
        obj['i' + ano] = '🚧'
      } else {
        obj['i' + ano] = '🚨'
      }
      obj['p' + ano] = (obj['f' + ano] / Number(populacao) * 100).toFixed(2)

      return obj
    }
  },
  created () {
    this.$nextTick(() => {
      this.$validator.validateAll()
    })
  },
  destroyed: function () {}
}
// let promises = null;
// cidades.forEach(cidade =>{
//   let p =new Promise((resolve, reject) => {
//   reject("reject");
// });
//   promises.push(p);
// });

// Promise.all(promises).then()
</script>

<style lang="scss">
input[type="checkbox"]:disabled + label,
input[type="radio"]:disabled + label,
input[type="checkbox"]:disabled,
input[type="radio"]:disabled {
  cursor: not-allowed;
}
</style>

