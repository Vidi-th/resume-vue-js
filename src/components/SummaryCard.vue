<template>
  <v-container>
    <ApolloQuery 
      :query="searchFromStore !=''?(gql => gql`
        query MyQuery2($id: Int!) {
            summary_by_pk(id: $id) {
                id
                title
                resume
                cover
            }
        }
      `) : (gql =>gql`query MyQuery {
            summary {
                id
                title
                resume
                cover
            }
            }`
        )"
      :variables="searchComputed"
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
        <div v-if="data.summary_by_pk">
          <summary-card-item
          :data="data.summary_by_pk"
          :index="data.summary_by_pk.id"
          >
          </summary-card-item>
        </div>
        <div v-else-if="data.summary_by_pk == null && !data.summary">{{ "Belum ada summary" }}</div>
        <div v-if="data.summary">
          <summary-card-item
          v-for="(card, index) in data.summary" 
          :key="index"
          :data="card"
          :index="card.id"
          >
          </summary-card-item>
        </div>
      </div>

      <!-- No result -->
      <div v-else class="no-result apollo">Loading...</div>

    </template>
    </ApolloQuery>
  </v-container>
</template>

<script>
import SummaryCardItem from "@/components/SummaryCardItem.vue"

export default {
  setup() {
      
  },
  data: () => ({
      show: false,
  }),
  components: {
      SummaryCardItem,
  },
  computed: {
  searchComputed(){
    if(this.searchFromStore == ""){
      return {};
    }
    return {id: this.searchFromStore};
  },

  searchFromStore(){
    return this.$store.state.page;
  }
  },
}
</script>