<template>
    <v-form @submit="onSubmit">
        <v-text-field label="Username" v-model="name"></v-text-field>
        <v-text-field label="Password" v-model="password" :type="show1 ? 'text' : 'password'"></v-text-field>
        <v-btn color="green" type="submit">Login</v-btn>
    </v-form>
</template>

<script>
export default {
    name: "ValidateUser",
    data() {
        return {
            name: '',
            password: ''
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
                    password: this.password,
                }

                this.$emit('validate-user', newUser);

                this.name = ''
                this.password = ''
            }
        }
}
</script>