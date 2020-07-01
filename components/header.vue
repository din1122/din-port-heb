<template>
  <v-app-bar dense flat fixed class="app-bar" height="67px">
    <nuxt-link to="/">
      <v-toolbar-title>
        <img height="75px" src="/logo.png" />
      </v-toolbar-title>
    </nuxt-link>
    <v-spacer></v-spacer>
    <div>
      <Menu v-on:open-drawer="$emit('open-drawer')" />
    </div>
  </v-app-bar>
</template>

<script>
import Menu from "~/components/menu.vue";
export default {
  components: {
    Menu
  }
};
</script>

<style lang="scss" scoped>
.v-toolbar__title {
  margin-left: -10%;
}
</style>
