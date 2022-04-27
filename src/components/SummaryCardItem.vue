<template>
    <v-container>
        <v-card
        class="mx-auto"
        max-width="800"
        >
            <v-img
            :src= "data.cover"
            height="300px"
            ></v-img>

            <v-card-title>
            {{ data.title}}
            </v-card-title>

            <v-card-subtitle>
            Section {{ index+1 }}
            </v-card-subtitle>

            <v-card-actions>
            <v-btn
                color="blue lighten-2"
                text
            > 
                <router-link :to="{ name: 'Detail', params: {index: data.id}}">
                    Detail
                </router-link>
            </v-btn>

            <v-spacer></v-spacer>

            <v-btn
                icon
                @click="show = !show"
            >
                <v-icon>{{ show ? 'mdi-chevron-up' : 'mdi-chevron-down' }}</v-icon>
            </v-btn>
            </v-card-actions>

            <v-expand-transition>
            <div v-show="show">
                <v-divider></v-divider>

                <v-card-text>
                {{ data.resume }}
                </v-card-text>
            </div>
            </v-expand-transition>

        </v-card>
    </v-container>
</template>

<script>
export default {
    name: "SummaryCardItem",
    data() {
        return {
            show: false,
        };
    },
    props: {
        data: Object,
        index: Number,
    },
    computed: {
        imageComputed() {
            return this.data.cover
        }
    }
}
</script>