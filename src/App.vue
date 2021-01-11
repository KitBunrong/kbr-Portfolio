<template>
  <v-app>
    <Navigation :flat="flat" />
    <v-main>
      <Work />
    </v-main>
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
      if (typeof window === "undefined") return;
      const top = window.pageYOffset || e.target.documentElement.scrollTop || 0;
      this.fab = top > 60;
    },
  },
};
</script>
