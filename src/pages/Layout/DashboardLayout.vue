<template>
  <div class="wrapper" :class="{ 'nav-open': $sidebar.showSidebar }">
    <notifications></notifications>

    <side-bar v-if="$auth.isAuthenticated">
      <mobile-menu slot="content"></mobile-menu>
      <sidebar-link to="/user">
        <md-icon>person</md-icon>
        <p>Meu Perfil</p>
      </sidebar-link>
      <sidebar-link to="/dashboard">
        <md-icon>dashboard</md-icon>
        <p>Resumo</p>
      </sidebar-link>      
      <sidebar-link to="/configuracoes">
        <md-icon>settings</md-icon>
        <p>Configurações</p>
      </sidebar-link>
    </side-bar>

    <side-bar v-if="!$auth.isAuthenticated && !$auth.loading">
      <mobile-menu slot="content"></mobile-menu>
    </side-bar>

    <div class="main-panel">
      <top-navbar></top-navbar>

      <dashboard-content> </dashboard-content>

      <content-footer v-if="!$route.meta.hideFooter"></content-footer>
    </div>
  </div>
</template>
<style lang="scss"></style>
<script>
import TopNavbar from "./TopNavbar.vue";
import ContentFooter from "./ContentFooter.vue";
import DashboardContent from "./Content.vue";
import MobileMenu from "@/pages/Layout/MobileMenu.vue";

export default {
  components: {
    TopNavbar,
    DashboardContent,
    ContentFooter,
    MobileMenu
  },
  
};
</script>
