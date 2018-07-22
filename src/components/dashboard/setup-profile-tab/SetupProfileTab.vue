<template>
  <div class="setup-profile-tab dashboard-tab">
    <vuestic-wizard
      :steps="steps"
      wizard-layout="vertical"
      :wizard-type="wizardType">
      <div slot="page1" class="form-wizard-tab-content">
        <h4>Funcionalidade #1</h4>
        <p>Manduma pindureta quium dia nois paga. Interagi no mé, cursus quis, vehicula ac nisi. Si u mundo tá muito paradis? Toma um mé que o mundo vai girarzis! Paisis, filhis, espiritis santis. </p>
        <div class="form-group with-icon-right"
             :class="{'has-error': errors.has('name'), 'valid': isFormFieldValid('name')}">
          <div class="input-group">
            
            
          </div>
        </div>
      </div>
      <div slot="page2" class="form-wizard-tab-content">
        <h4>Funcionalidade #2</h4>
        <p>Mussum Ipsum, cacilds vidis litro abertis. Tá deprimidis, eu conheço uma cachacis que pode alegrar sua vidis. Quem num gosta di mé, boa gentis num é. Per aumento de cachacis, eu reclamis. Todo mundo vê os porris que eu tomo, mas ninguém vê os tombis que eu levo!</p>

        
      </div>
      <div slot="page3" class="form-wizard-tab-content">
        <h4>Funcionalidade #3</h4>
        <p>
          Detraxit consequat et quo num tendi nada. Copo furadis é disculpa de bebadis, arcu quam euismod magna. Quem manda na minha terra sou euzis! Diuretics paradis num copo é motivis de denguis. 
        </p>
      </div>
      <div slot="wizardCompleted"
           class="form-wizard-tab-content wizard-completed-tab">
        <h4>Algum texto justificando o uso dessas funcionalidades</h4>
        <p>
          A ordem dos tratores não altera o pão duris. Vehicula non. Ut sed ex eros. Vivamus sit amet nibh non tellus tristique interdum. Mauris nec dolor in eros commodo tempor. Aenean aliquam molestie leo, vitae iaculis nisl. Sapien in monti palavris qui num significa nadis i pareci latim. 
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
            label: 'Funcionalidade #1',
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
            label: 'Funcionalidade #2',
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
            label: 'Funcionalidade #3',
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
