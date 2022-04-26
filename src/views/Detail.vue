<template>
  <v-container>
    <ApolloQuery
      :query="gql => gql`
        query MyQuery($id: Int!) {
          summary_by_pk(id: $id) {
            id
            title
            additional_equipments {
              id
              detail
              link_file
              screenshot
            }
          }
        }
      `"
      :variables="{ id: summary }"
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
        <H1>{{ data.summary_by_pk.title }}</H1> 
        <br>
        <v-row justify="center">
          <v-expansion-panels accordion>

            <!-- Expansion Panel Untuk Detail -->
            <v-expansion-panel
              v-for="tree in data.summary_by_pk.additional_equipments"
              :key="`detail`+tree.id"
            >
            <label v-if="tree.detail">
              <v-expansion-panel-header>Detail Rangkuman</v-expansion-panel-header>
              <v-expansion-panel-content>
                {{ tree.detail }}
              </v-expansion-panel-content>
            </label>
            </v-expansion-panel>

            <!-- Expansion Panel Untuk Link Praktikum -->
            <v-expansion-panel
              v-for="tree in data.summary_by_pk.additional_equipments"
              :key="`linkPrakikum`+tree.id"
            >
            <label v-if="tree.link_file">
              <v-expansion-panel-header>Link Praktikum</v-expansion-panel-header>
              <v-expansion-panel-content>
                <a :href="tree.link_file"> {{ tree.link_file}}</a>
              </v-expansion-panel-content>
            </label>
            </v-expansion-panel>

            <!-- Expansion Panel Untuk Screenshot -->
            <v-expansion-panel
            v-for="(tree, index) in data.summary_by_pk.additional_equipments"
            :key="`screenshot`+tree.id"
            >
            <label v-if="tree.screenshot">
              <v-expansion-panel-header>Screenshot Praktikum {{ index +1 }}</v-expansion-panel-header>
              <v-expansion-panel-content>
                <v-img
                :src= "tree.screenshot"
                ></v-img>
              </v-expansion-panel-content>
            </label>
            </v-expansion-panel>

          </v-expansion-panels>
        </v-row>
      </div>

      <!-- No result -->
      <div v-else class="no-result apollo">Loading...</div>

    </template>
    </ApolloQuery>

    
  </v-container>
</template>

<script>
  export default {
    data: () => ({
              
    }),

    computed:{
      summary() {
        return this.$route.params.index;
      }
    },
  }
</script>