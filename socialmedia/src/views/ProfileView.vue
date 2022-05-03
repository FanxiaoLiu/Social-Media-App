<template>
    <ProfileDisplay :user='user' />
</template>

<script>
import ProfileDisplay from '../components/Profile.vue'

export default {
    name:'ProfileView',
    components: {
        ProfileDisplay
    },
    data() {
        return {
            user: []
        }
    },
    methods: {
        async fetchUserbyID(id) {
            const res = await fetch(`api/users/${id}`)
            const data = await res.json()

            return data
        },
    },
    async created() {
        let user = sessionStorage.getItem('currentUser')
        this.user = await this.fetchUserbyID(user);
    }
}
</script>