<template>
    <v-app>
        <v-card contained-text>
            <v-card-title>{{ user.name }}</v-card-title>
            <v-card-subtitle>{{ user.email }}</v-card-subtitle>
            <v-card-text>{{ user.id }}</v-card-text>
            <v-card-text>Followers: {{ user.followers }}</v-card-text>
            <v-card-actions><v-btn @click="followUser" variant="outlined">
                Follow/Unfollow
            </v-btn></v-card-actions>
        </v-card>
    </v-app>
</template>

<script>
export default {
    name: "ProfileDisplay",
    props: {
        user: Object,
    },
    methods: {
        async followUser() {
            let followerID = sessionStorage.getItem('userID')

            const user = sessionStorage.getItem('currentUser')

            console.log(user)

            const res = await fetch(`api/users/${user}`)
            let data = await res.json()
            console.log(data)

            // Creating an array of all the followers

            let fArray = data.followers.split(',');

            let doesFollow = false;

            for (let i = 0; i < fArray.length; i++) {
                if (followerID == fArray[i]) {
                    doesFollow = true;
                    alert('You already follow this user. This user will now be unfollowed')
                    console.log(data.followers.length)
                    if (data.followers.length == 1)
                        data.followers = ''
                    else 
                        data.followers = data.followers.substring(0,data.followers.indexOf(fArray[i])) + data.followers.substring(data.followers.indexOf(fArray[i])+2)
                    break
                }
            }

            console.log(doesFollow)

            if (!doesFollow) {
                if (data.followers === '') {
                    data.followers = data.followers + followerID;
                }
                else {
                    data.followers = data.followers + ',' + followerID;
                }
            }

            console.log(data.followers)

            // eslint-disable-next-line
            const resp = await fetch(`api/users/${user}`, {
                method: "PATCH",
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify( {followers: data.followers} )
            })
            .then(response => response.json())
            .then(resp => {
                console.log('Success:', resp);
            })
        }
    }

}
</script>