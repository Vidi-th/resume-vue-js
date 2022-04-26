<template>
<div>
    <br>
    <summary-card/>
</div>
</template>

<script>
import SummaryCard from "@/components/SummaryCard.vue"

export default {
    name: "Summary",
    components: {
        SummaryCard
    },
    data: () => ({
        show: false,
    }),
}
</script>

<style scoped>

</style>