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
      <sidebar-link to="/table">
        <md-icon>content_paste</md-icon>
        <p>Tabela</p>
      </sidebar-link>
      <sidebar-link to="/typography">
        <md-icon>library_books</md-icon>
        <p>Typography</p>
      </sidebar-link>
      <sidebar-link to="/icons">
        <md-icon>bubble_chart</md-icon>
        <p>Icons</p>
      </sidebar-link>
      <sidebar-link to="/maps">
        <md-icon>location_on</md-icon>
        <p>Maps</p>
      </sidebar-link>
      <sidebar-link to="/notifications">
        <md-icon>notifications</md-icon>
        <p>Notifications</p>
      </sidebar-link>
      <sidebar-link to="/upgrade" class="active-pro">
        <md-button class="md-icon-button" @click.prevent="logout">
           <md-icon>unarchive</md-icon>
           <p>Sair</p>
        </md-button> 
      </sidebar-link>
    </side-bar>
    
    <side-bar v-if="!$auth.isAuthenticated && !$auth.loading">
      <mobile-menu slot="content"></mobile-menu>
        <sidebar-link to="/login">
	   <md-button class="md-icon-button" @click.prevent="login">
              <md-icon>person</md-icon>
              <p>Entrar</p>
           </md-button>
        </sidebar-link>
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
  methods: {
    login(){
      this.$auth.loginWithRedirect();
    },
    logout(){
      this.$auth.logout();
      this.$router.push({ path: "/" });
    }
  }
};
</script>
