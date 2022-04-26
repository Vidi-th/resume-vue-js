<template>
  <v-app>

    <v-navigation-drawer
      v-model="drawer"
      fixed
      app
      clipped
      color="#0d1b66"
      dark
    >
      <v-list
        nav
        dense
      >
        <v-list-item-group
          v-model="group"
          active-class="deep-purple--text text--accent-4"
        >
          <v-list-item v-for="(item, index) in items" :key=index>
            <v-list-item-title> {{ item }} </v-list-item-title>
          </v-list-item>

        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      color="blue"
      elevation="4"
      shaped
      clipped-left
      fixed
      dark
    >
      <v-app-bar-nav-icon 
        @click.stop="drawer = !drawer">
      </v-app-bar-nav-icon>

      <div class="d-flex align-center">
        <v-img
          alt="Altera Logo"
          class="shrink mr-2"
          contain
          src="@/assets/logo_altera.png"
          transition="scale-transition"
          width="100"
        />

        <v-spacer></v-spacer>
        <v-app-bar-title
        class="font-weight-bold"
        > SUMMARY VIDITYAR </v-app-bar-title>
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/Vidi-th/Vue_Vidityar-Adith-Nugroho.git"
        target="_blank"
        text
      >
        <span class="mr-2">see more here</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <router-view/>

    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    items: ["general", "business", "sport", "entertainment", "health", "science", "technology"],
    drawer: false,
    group: null,
  }),

  watch: {
    group () {
      this.drawer = false
    },
  },
};
</script>

<style>
v-main{
  padding-top: 20px;
}
</style>