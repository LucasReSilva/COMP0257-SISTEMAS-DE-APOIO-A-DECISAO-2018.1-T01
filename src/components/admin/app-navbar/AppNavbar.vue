<template>

  <vuestic-navbar>
    <header-selector slot="selector" :isOpen.sync="valueProxy"/>
    <span slot="logo" class="logo d-sm-none d-md-block"></span>
    <span slot="center">
      <div><h5>{{$t('navbar.messageUs')}}</h5><a href="#">{{$t('navbar.messageSmall')}}</a></div>
    </span>
    <!--<message-dropdown/>
    <notification-dropdown/> -->
    <language-dropdown/>
    <profile-dropdown>
      <!--img src="http://i.imgur.com/nfa5itq.png"/-->
      <img  src="https://i.imgur.com/TLm0Pzc.png"/>
    </profile-dropdown>
  </vuestic-navbar>

</template>

<script>
  import VuesticNavbar from '../../../vuestic-theme/vuestic-components/vuestic-navbar/VuesticNavbar'
  import HeaderSelector from './components/HeaderSelector'
  import LanguageDropdown from './components/dropdowns/LanguageDropdown'
  import ProfileDropdown from './components/dropdowns/ProfileDropdown'
  import NotificationDropdown from './components/dropdowns/NotificationDropdown'
  import MessageDropdown from './components/dropdowns/MessageDropdown'

  export default {
    name: 'app-navbar',

    components: {
      VuesticNavbar,
      HeaderSelector,
      MessageDropdown,
      NotificationDropdown,
      LanguageDropdown,
      ProfileDropdown
    },
    props: {
      isOpen: {
        type: Boolean,
        required: true
      }
    },
    computed: {
      valueProxy: {
        get () {
          return this.isOpen
        },
        set (opened) {
          this.$emit('toggle-menu', opened)
        },
      },
    },
  }
</script>
<style lang="scss">
  h5 {
      display: inline;
      margin-right: 10px;
  }
</style>
