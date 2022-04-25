<template>
    <v-btn color = "secondary" @click="loginClick">Login</v-btn>
    <v-btn color = "secondary" @click="signupClick">Sign Up</v-btn>

    <div v-show="showSignUp">
        <AddUser @add-user="addUser" />
    </div>
    
    <div v-show="showLogin">
        <ValidateUser @validate-user="validateUser" />
    </div>
</template>

<script>
import AddUser from '../components/AddUser.vue'
import ValidateUser from '../components/ValidateUser.vue'

export default {
    name: "LoginView",
    data() {
        return {
            showSignUp: false,
            showLogin: false,
            users: []
        }
    },
    components: {
        AddUser,
        ValidateUser
    },
    methods: {
        signupClick() {
            this.showSignUp = true;
            this.showLogin = false;
        },
        loginClick() {
            this.showLogin = true;
            this.showSignUp = false;
        },
        async addUser(user) {
            const res = await fetch('api/users', {
            method: 'POST',
            headers: {
                'Content-type': 'application/json',
            },
            body: JSON.stringify(user),
        })

        const data = await res.json() 

        this.users = [...this.users, data]
        },
        async fetchUsers() {
        const res = await fetch('api/users')
        const data = await res.json()

        return data
        },
        async fetchUserbyID(id) {
            const res = await fetch(`api/users/${id}`)
            const data = await res.json()

            return data
        },
        async validateUser(loginCred) {
            const userList = await fetch('api/users')
            const userListJson = await userList.json()
            let userLogin;

            for (let i = 1; i < userListJson.length+1; i++) {
                const res = await fetch(`api/users/${i}`)
                const data = await res.json()

                console.log(data.name)
                console.log(loginCred.name)

                if (data.name == loginCred.name) {
                    const res1 = await fetch(`api/users/${i}`)
                    userLogin = await res1.json()
                }
            }
            const dbpassword = userLogin.password

            console.log(loginCred.password);
            console.log(dbpassword)

            if (dbpassword == loginCred.password) {
                sessionStorage.setItem("userID", userLogin.id)
                console.log(sessionStorage.getItem('userID'))
            }
            else {
                alert('The Credentials are incorrect.')
            }
        }
    },
    async created() {
        this.users = await this.fetchUsers();
    }
}
</script>