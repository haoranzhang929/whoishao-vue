<template>
  <v-app>
    <Navbar/>
    <v-content>
      <router-view></router-view>
    </v-content>
    <Footer/>
    <Particle/>
  </v-app>
</template>

<script>
import Navbar from "@/components/Navbar";
import Footer from "@/components/Footer";
import Particle from "@/components/Particle";

export default {
  name: "App",
  components: { Navbar, Footer, Particle },
  data() {
    return {
      //
    };
  }
};
</script>

<style>
html {
  overflow: hidden;
}

.v-content {
  z-index: 1;
}
</style>

