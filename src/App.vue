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
        active-class="Aqua--text text--accent-4"
      >
      <ApolloQuery
        :query="gql => gql`
          query Title {
            summary {
              id
              title
            }
          }
        `"
      >

      <template v-slot="{ result: { loading, error, data } }">

        <!-- Loading -->
        <div v-if="loading" class="loading apollo">Loading...</div>

        <!-- Error -->
        <div v-else-if="error" class="error apollo">An error occurred
          {{ error }}
        </div>

        <!-- Result -->
        <div v-else-if="data" class="result apollo"> 
                
          <router-link 
          style="text-decoration: none; color: inherit;"
          :to="{ name: 'Summary'}" >
          <v-list-item v-for="(item, index) in data.summary" :key=index @click="press(item.id)">
            <v-list-item-title> 
              {{ item.title }} 
            </v-list-item-title>
          </v-list-item>
          </router-link>
        </div>
        <!-- No result -->
        <div v-else class="no-result apollo">No result :(</div>

      </template>
      </ApolloQuery>
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
      <router-link :to="{ name: 'Summary'}" >
      <v-img
        alt="Altera Logo"
        class="shrink mr-2"
        contain
        src="@/assets/logo_altera.png"
        transition="scale-transition"
        width="100"
        @click="home"
      />
      </router-link >

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
    drawer: false,
    group: null,
    tekan: false,
  }),
  methods: {
    home(){
      this.$store.commit('setPage', "");
    },
    press(id){
      this.tekan = !this.tekan;
      this.$store.commit('setPage', id);
    }
  },
  watch: {
    group () {
      this.drawer = false
    },
  },
  action: {

  },
};
</script>

<style>
v-main{
  padding-top: 20px;
}
</style>