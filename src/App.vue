<template>
  <v-app>
    <Navigation :flat="flat" />
    <v-main>
      <Work />
    </v-main>
    <v-fab-transition>
      <!-- 
        v-show="fab"
        + used for toggle visibility of element only if fab=true.
       -->
      <v-btn
        fab
        v-show="fab"
        v-scroll="onScroll"
        fixed
        bottom
        right
        @click="toTop"
      >
        <v-icon>mdi-arrow-up</v-icon>
      </v-btn>
    </v-fab-transition>
  </v-app>
</template>

<script>
import Navigation from "./components/Navigation";
import Work from "./components/Work";
export default {
  name: "App",

  components: {
    Navigation,
    Work,
  },

  data: () => ({
    flat: false,
    fab: false,
  }),

  created() {
    const top = window.pageYOffset || 0;
    if (top <= 60) {
      this.flat = true;
    }
  },

  watch: {
    fab(value) {
      if (value) {
        this.flat = false;
      } else {
        this.flat = true;
      }
    },
  },

  methods: {
    onScroll(e) {
      // if(typeof window === "undefined") return
      // + using "typeof" to prevent error "Reference: window is not defined"
      //   In Node.js world, window is not defined, window is only available in browsers.
      // + "typeof" won't try to evaluate "window", it will only try to get its type,
      //   in our case in Node.js: "undefined".
      if (typeof window === "undefined") return;
      // window.pageYOffset == window.top.scrollY == e.target.documentElement.scrollTop;
      const top = window.pageYOffset || e.target.documentElement.scrollTop || 0;
      this.fab = top > 60;
    },
    toTop() {
      this.$vuetify.goTo(0);
    },
  },
};
</script>
