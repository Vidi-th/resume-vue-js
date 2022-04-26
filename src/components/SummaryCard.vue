<template>
    <v-container>
    
    <ApolloQuery 
      :query="search!=''?(gql => gql`
        query MyQuery2($id: Int!) {
        summary_by_pk(id: $id) {
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
          <div v-if="data.summary_by_pk">{{ data.summary_by_pk.title }}</div>
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
        <div v-else class="no-result apollo">No result :(</div>
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
        search: "",
    }),
    components: {
        SummaryCardItem,
    },
    computed: {
    searchComputed(){
      console.log("Search computed :", this.search);
      if(this.search !== ""){
        return {id: this.search};
      }
      return {};
    }
    }
}
</script>