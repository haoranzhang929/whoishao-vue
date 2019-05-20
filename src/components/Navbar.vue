<template>
  <nav>
    <v-toolbar prominent class="light-blue darken-3">
      <v-toolbar-side-icon class="white--text" @click="drawer = !drawer"></v-toolbar-side-icon>

      <v-toolbar-title class="text-uppercase white--text">
        <v-img src="/logo.svg" max-width="40px" min-width="40px"></v-img>
      </v-toolbar-title>

      <v-spacer></v-spacer>

      <v-toolbar-items class="hidden-sm-and-down">
        <v-btn
          flat
          icon
          color="white"
          v-for="link in links"
          :key="link.icon"
          router
          :to="link.route"
        >
          <v-icon>{{ link.icon }}</v-icon>
        </v-btn>
      </v-toolbar-items>

      <v-toolbar-items class="hidden-md-and-up">
        <v-menu offset-y>
          <v-btn flat slot="activator" color="white">
            <v-icon left>expand_more</v-icon>
            <span>Menu</span>
          </v-btn>
          <v-list>
            <v-list-tile v-for="link in links" :key="link.icon" router :to="link.route">
              <v-list-tile-action>
                <v-icon>{{ link.icon }}</v-icon>
              </v-list-tile-action>

              <v-list-tile-content>
                <v-list-tile-title>{{ link.text }}</v-list-tile-title>
              </v-list-tile-content>
            </v-list-tile>
          </v-list>
        </v-menu>
      </v-toolbar-items>
    </v-toolbar>

    <v-navigation-drawer v-model="drawer" app temporary width="250">
      <v-layout column align-center>
        <v-flex class="mt-3">
          <v-avatar size="80">
            <img src="/portrait.jpg">
          </v-avatar>
        </v-flex>
        <v-flex>
          <p class="black--text title mt-3 text-xs-center">Haoran Zhang</p>
        </v-flex>
        <v-flex class="mb-2">
          <a
            class="grey--text subheading text-xs-center font-weight-light email"
            href="mailto:haoranzhang@icloud.com"
          >haoranzhang@icloud.com</a>
        </v-flex>
      </v-layout>
      <v-list>
        <v-list-tile
          class="grey--text text--darken-2"
          active-class="blue lighten-4 blue--text text--darken-3"
          v-for="link in links"
          :key="link.text"
          router
          :to="link.route"
          ripple
        >
          <v-list-tile-action>
            <v-icon>{{ link.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>{{ link.text }}</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      drawer: false,
      links: [
        { icon: "home", text: "Home", route: "/" },
        { icon: "collections", text: "Projects", route: "/projects" },
        { icon: "contact_mail", text: "Contact", route: "/contact" },
        { icon: "info", text: "About", route: "/about" }
      ]
    };
  }
};
</script>

<style scoped>
.email {
  text-decoration: underline;
}
</style>
