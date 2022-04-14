<template>
    <div :key="card.id" v-for="card in cards">
        <Card :card="card" />
    </div>
</template>

<script>
import Card from "./Card"
export default {
    name: "ManyCards",
    props: {
        cards: Array
    },
    components: {
        Card
    }
}
</script>