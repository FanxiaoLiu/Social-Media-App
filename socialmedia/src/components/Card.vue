<template>
    <v-container>
        <v-card>
            <v-card-title>{{ card.title }}</v-card-title>
            <v-card-subtitle>{{ card.desc }}</v-card-subtitle>
            <v-card-text>{{ card.content }}</v-card-text>
        </v-card>
    </v-container>
</template>

<script>
export default {
    name: "SingleCard",
    props: {
        card: Object,
    },

}
</script>