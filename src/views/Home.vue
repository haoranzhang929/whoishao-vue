<template>
  <v-container align-content-center fluid fill-height>
    <v-layout row wrap align-center>
      <v-flex xs12 md6 align-self-start class="display-3 secondary--text text-xs-center home-item">
        <VueTyper/>
      </v-flex>
      <v-flex xs12 md6 align-self-end class="display-4 text-xs-center home-item">
        <Three/>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import { VueTyper } from "vue-typer";
import Three from "@/components/Three";

export default {
  components: { Three, VueTyper }
};
</script>

<style scoped>
@media (max-width: 960px) {
  .home-item {
    align-self: center;
  }
}
</style>

