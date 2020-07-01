<template>
  <div>
    <div
      class="inline-menu"
      @mouseenter="Hovermenu"
      @mouseleave="mouseleft"
      v-on:click="$emit('open-drawer')"
    >
      <span class="menu btn" :class="{ active: ishover, whiteMenu: show }">MENU</span>
      <svg
        viewBox="0 -35 90 120"
        :class="{ active: svghover, whiteMenu: show }"
        class="btn"
        fill="black"
        width="30"
        height="20"
      >
        <rect class="rect" :y="FirstY" width="100" height="9" />
        <rect class="rect" y="30" width="100" height="9" />
        <rect class="rect" :y="lastY" width="100" height="9" />
      </svg>
    </div>
<!--
    <transition name="overlay">
      <div class="overlay" v-if="show">
        <div class="overlay-content" @click="show = false">
          <nav>
            <nuxt-link @click.native="show = false" to="/">
              <li>projects</li>
            </nuxt-link>
            <nuxt-link @click.native="show = false" to="/about">
              <li>About</li>
            </nuxt-link>
            <nuxt-link @click.native="show = false" to="/contact">
              <li>Contact</li>
            </nuxt-link>
            <a @click="show = false" href="#">
              <li>Behance</li>
            </a>
            <a @click="show = false" href="#">
              <li>Instagram</li>
            </a>
            <a @click="show = false" href="#">
              <li>Dirbbble</li>
            </a>
          </nav>
        </div>
      </div>
    </transition>
    -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      menuItems:[
        {url:"/", title:"Home"},
        {url:"/about", title:"About"},
        {url:"/contact", title:"Contact"},
      ],
      show: false,
      svghover: false,
      ishover: false,
      drawer: false,
      FirstY: 0,
      lastY: 60,
      fillColor: "black"
    };
  },
  methods: {
    Hovermenu() {
      this.svghover = true;
      this.ishover = true;
      this.FirstY = -5;
      this.lastY = 65;
    },
    mouseleft() {
      this.svghover = false;
      this.ishover = false;
      this.FirstY = 0;
      this.lastY = 60;
    }
  }
};
</script>

<style lang="scss" scoped>
.overlay-enter-to,
.overlay-enter-active {
  opacity: 1;
  transition: all 0.35s;
}
.overlay-leave-to,
.overlay-enter {
  opacity: 0;
  transition: all 0.35s;
}
.overlay {
  height: 100vh;
  width: 100%;
  background: #0d072bd5;
  left: 0;
  right: 0;
  z-index: 10;
  bottom: 0;
  top: 0;
  position: absolute;
  display: block;
}
.svg {
  fill: black;
  display: inline;
}
.rect {
  transition: all 0.3s;
}

.menu {
  transition: all 0.1s;
  display: inline;
}
.active {
  fill: gray;
  color: gray;
}
.whiteMenu {
  color: white;
  fill: white;
  z-index: 99;
}
.inline-menu {
  display: flex;
  justify-content: center;
  flex-direction: row;
  z-index: 5;
  cursor: pointer;
}
</style>
