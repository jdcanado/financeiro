<template>
  <div
    class="sidebar"
    :data-color="activeColor"
    :data-image="backgroundImage"
    :style="sidebarStyle"
  >
    <div class="logo" v-if="$auth.isAuthenticated">
      <md-card class="md-card-profile">
        <div class="md-card-avatar">
          <img class="img" :src="$auth.user.picture" />
        </div>
        <div>
          <h2>{{ $auth.user.name }}</h2>
          <h6>{{ $auth.user.email }}</h6>
        </div>
      </md-card>
    </div>
    <div class="logo" v-if="!$auth.isAuthenticated">
      <md-card class="md-card-profile">
        <div class="md-card-avatar">
          <img class="img" :src="imgLogo" />
        </div>
        <div>
          <h3 style="font-family: 'Special Elite', cursive;">JDC Financeiro</h3>
          <div>Esqueceu a senha?</div><a>Clique aqui</a>
        </div>
      </md-card>
    </div>
    <div class="sidebar-wrapper">
      <slot name="content"></slot>
      <md-list class="nav">
        <!--By default vue-router adds an active class to each route link. This way the links are colored when clicked-->
        <slot>
          <sidebar-link
            v-for="(link, index) in sidebarLinks"
            :key="link.name + index"
            :to="link.path"
            :link="link"
          >
          </sidebar-link>
        </slot>
      </md-list>
    </div>
  </div>
</template>
<script>
import SidebarLink from "./SidebarLink.vue";

export default {
  components: {
    SidebarLink
  },
  props: {
    title: {
      type: String,
      default: "Vue MD"
    },
    fontLogo: {
      type: String,
      default: "Special Elite"
    },
    backgroundImage: {
      type: String,
      default: require("@/assets/img/sidebar-2.jpg")
    },
    imgLogo: {
      type: String,
      default: require("@/assets/img/logo_jdcanado_editado_quadrado_cubo.png")
    },
    activeColor: {
      type: String,
      default: "green",
      validator: value => {
        let acceptedValues = ["", "purple", "blue", "green", "orange", "red"];
        return acceptedValues.indexOf(value) !== -1;
      }
    },
    sidebarLinks: {
      type: Array,
      default: () => []
    },
    autoClose: {
      type: Boolean,
      default: true
    }
  },
  provide() {
    return {
      autoClose: this.autoClose
    };
  },
  computed: {
    sidebarStyle() {
      return {
        backgroundImage: `url(${this.backgroundImage})`
      };
    },
    logoStyle() {
      return {
        fontFamily: `url(${this.fontLogo})`
      };
    }	
  }
};
</script>
<style>
@media screen and (min-width: 991px) {
  .nav-mobile-menu {
    display: none;
  }
}
@import url("https://fonts.googleapis.com/css?family=Special+Elite&display=swap");
</style>
