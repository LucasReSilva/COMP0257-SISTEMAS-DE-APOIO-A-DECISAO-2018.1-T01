<template>
  <div class="setup-profile-tab dashboard-tab">
    <vuestic-wizard
      :steps="steps"
      wizard-layout="vertical"
      :wizard-type="wizardType">
      <div slot="page1" class="form-wizard-tab-content">
        <h4>Mapa de calor dos casos de dengue</h4>
        <p>O mapa de calor permite visualizar as áreas com maior ocorrência de casos de dengue. Quanto maior a região vermelha em uma dada região, maior é a quantidade de casos de dengue. Com isso os gestores podem aplicar mais recursos nessas áreas e otimizar o combate a dengue. </p>
        <div class="form-group with-icon-right"
             :class="{'has-error': errors.has('name'), 'valid': isFormFieldValid('name')}">
          <div class="input-group">
            
            
          </div>
        </div>
      </div>
      <div slot="page2" class="form-wizard-tab-content">
        <h4>Ranking da taxa de incidência de casos da dengue</h4>
        <p>O ranking de indicadores de incidência traz um forma de comparar a situação das cidades com um indicador nacional. Devido a falta de dados populacionais, o calculo de todos os anos utilizara os dados da população de 2017.</p> <p>
Para calcular a incidência, divide-se o número de notificações (ou seja, o número de novos casos da doença) pela população do município e multiplica-se este valor por 100 mil. </p>
<p>O Ministério da Saúde considera três níveis de incidência de dengue: baixa (menos de 100 casos/100 mil habitantes), média (de 100 a 300 casos/100 mil habitantes) e alta (mais de 300 casos/100 mil habitantes).</p>
<p>A taxa de incidência é, portanto, um importante indicador de alerta e ajuda a orientar as ações de combate à dengue.</p>

        
      </div>
      <div slot="page3" class="form-wizard-tab-content">
        <h4>Ranking da porcentagem de casos de dengue</h4>
        <p>
          Esse ranking apresenta o número de casos de dengue, a população e a porcentagem da população que teve dengue no ano de 2017. Esse ranking ajuda a entender o qual impactante o número de casos de dengue é em uma certa cidade. 
        </p>
      </div>
      <div slot="wizardCompleted"
           class="form-wizard-tab-content wizard-completed-tab">
        <h4>Objetivos</h4>
        <p>
          O objetivo do SADengue é presentar informações importantes sobre a doença, como a taxa de incidência na população, afim de facilitar a tomada de decisão relacionada a demanda de recursos a fim de diminuir os casos de dengue nas áreas mais afetadas. Espera-se alcançar os objetivos por meio da exibição de mapa de calor e rankings das cidades com maior incidência da doença. 
        </p>
      </div>
    </vuestic-wizard>
  </div>
</template>

<script>
  import CountriesList from 'data/CountriesList'

  export default {
    name: 'setup-profile-tab',
    props: {
      wizardType: {
        default: 'rich'
      },
    },
    data () {
      return {
        steps: [
          {
            label: '#1 Mapa de calor',
            slot: 'page1',
            onNext: () => {
              // this.validateFormField('name')
              return true
            },
            isValid: () => {
              // return this.isFormFieldValid('name')
              return true
            }
          },
          {
            label: '#2 Ranking da taxa de incidência',
            slot: 'page2',
            onNext: () => {
              // this.$refs.selectedCountrySelect.validate()
              return true
            },
            isValid: () => {
              // return this.$refs.selectedCountrySelect.isValid()
              return true
            }
          },
          {
            label: '#3 Ranking da porcentagem de casos',
            slot: 'page3'
          }
        ],
        selectedCountry: '',
        name: '',
        countriesList: CountriesList
      }
    },
    methods: {
      isFormFieldValid (field) {
        return true
      },
      validateFormField (fieldName) {
        return true
      }
    }
  }
</script>

<style lang="scss" scoped>
  .form-group {
    min-width: 200px;
    max-width: 360px;
    width: 80%;
  }

  .wizard-completed-tab {
    @include media-breakpoint-up(md) {
      margin-top: -$tab-content-pt;
    }
  }

</style>
