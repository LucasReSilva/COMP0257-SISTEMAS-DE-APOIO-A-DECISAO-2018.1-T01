<template>


  <div class="overview-tab dashboard-tab">
    <div class="d-flex overview-row flex-row w-100 justify-content-sm-around justify-content-xs-start">
        <div class="overview-col">
    A dengue é uma doença que ainda afeta boa parte da população brasileira, segundo o boletim epidemiológico (Ministério da Saúde 2018)  até a sétima semana de 2018, período que corresponde 31/12/2017 a 17/02/2018, foram registrados 32.161 casos prováveis de dengue no país. Casos prováveis para o Ministério da Saúde são os casos notificados, excluindo-se os descartados, por diagnóstico laboratorial negativo, com coleta oportuna ou diagnosticados para outras doenças. Comparando os dados desse período de 2018 com o mesmo período de anos anteriores, o número de casos atuais é inferior, mas continua preocupante pois ainda apresentam muitas ocorrências. Isso mostra que a doença ainda é um empecilho para saúde dos brasileiros. 
  </div>

    </div>
  </div>
</template>

<script>
  export default {
    name: 'features-tab'
  }
</script>

<style lang="scss" scoped>
  .overview-item {
    display: flex;
    align-items: center;
    height: 55px;
    margin-bottom: 3rem;
    padding-right: 1rem;
    font-size: 1.25rem;
    font-weight: bold;

    .overview-icon-container {
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: row;
      min-width: 85px;
      max-width: 85px;
      height: 100%;
    }
  }

  .overview-row {
    @include media-breakpoint-down(xs) {
      flex-wrap: wrap;
    }
  }

  .overview-col:first-child {
    margin-left: 2rem;
    @include media-breakpoint-down(md) {
      margin-left: 0;
    }
  }

  .explore-btn {
    margin-top: 6rem;
    margin-bottom: 1rem;
  }

</style>
