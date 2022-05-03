<template>
    <v-container>
        <v-card>
            <v-card-title>{{ card.title }}</v-card-title>
            <v-card-subtitle>{{ card.desc }} <br /> Posted by: {{card.postUserID}}</v-card-subtitle>
            <v-card-text>{{ card.content }}</v-card-text>
            <v-card-actions><v-btn @click="visitUser" variant="outlined">
                <router-link to="/profile">Visit Profile</router-link>
            </v-btn></v-card-actions>
        </v-card>
    </v-container>
</template>

<script>
export default {
    name: "SingleCard",
    props: {
        card: Object,
    },
    methods: {
        visitUser() {
            sessionStorage.setItem('currentUser',this.card.postUserID)
        }
    }
}
</script>