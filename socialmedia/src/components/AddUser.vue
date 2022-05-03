<template>
    <v-form @submit="onSubmit">
        <v-text-field label="Username" v-model="name"></v-text-field>
        <v-text-field label="Email" v-model="email"></v-text-field>
        <v-text-field label="Password" v-model="password" :type="show1 ? 'text' : 'password'"></v-text-field>
        <v-btn color="green" type="submit">Sign-up</v-btn>
    </v-form>
</template>

<script>
export default {
    name: "AddUser",
    data() {
        return {
            name: '',
            email: '',
            password: '',
            followers: ''
        }
    },
    methods: {
            onSubmit(e) {
                e.preventDefault();
                
                if(!this.name) {
                    alert('Please add a text');
                    return
                }

                const newUser = {
                    // id: Math.floor(Math.random() * 100000),
                    name: this.name,
                    email: this.email,
                    password: this.password,
                    followers: ''
                }

                this.$emit('add-user', newUser);

                this.name = ''
                this.email = ''
                this.password = ''
            }
        }
}
</script>