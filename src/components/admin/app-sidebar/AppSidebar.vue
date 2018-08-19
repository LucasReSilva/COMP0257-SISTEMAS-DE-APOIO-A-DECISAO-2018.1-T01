<template>
  <vuestic-sidebar :hidden="isOpen">
    <template slot="menu">
      <sidebar-link
        :to="{ name: 'extra' }">
        <span slot="title">
          <span class="sidebar-menu-item-icon vuestic-icon vuestic-icon-extras"></span>
          <span>{{ $t('menu.extra') }}</span>
        </span>
      </sidebar-link>

       <sidebar-link
          :to="{ name: 'google-maps' }" v-show="!isDengueDataEmpty(this.$store.state.app.dengueData)">
          <span slot="title">
          <span class="sidebar-menu-item-icon vuestic-icon vuestic-icon-maps"></span>
          <span>{{ $t('menu.maps') }}</span>
        </span>
        </sidebar-link>
        <sidebar-link
        :to="{ name: 'tables' }" v-show="!isDengueDataEmpty(this.$store.state.app.dengueData)">
        <span slot="title">
          <span class="sidebar-menu-item-icon vuestic-icon vuestic-icon-tables"></span>
          <span>{{ $t('menu.tables') }}</span>
        </span>
      </sidebar-link>
      <dengue-form/>
    </template>

  </vuestic-sidebar>


</template>

<script>

  import VuesticSidebar from '../../../vuestic-theme/vuestic-components/vuestic-sidebar/VuesticSidebar'
  import SidebarLink from './components/SidebarLink'
  import SidebarLinkGroup from './components/SidebarLinkGroup'
  import dengueForm from '../DengueForm'


  export default {
    name: 'app-sidebar',
    components: {
      VuesticSidebar,
      SidebarLink,
      SidebarLinkGroup,
      dengueForm
    },
    props: {
      isOpen: {
        type: Boolean,
        required: true
      }
    },
    methods: {
      isDengueDataEmpty (obj) {
        return Object.keys(obj).length === 0 && obj.constructor === Object
      }
    }
  }

</script>
