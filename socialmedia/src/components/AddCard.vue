<template>
    <v-form @submit="onSubmit">
        <v-text-field label="Post Title" v-model="title"></v-text-field>
        <v-text-field label="Post Description" v-model="desc"></v-text-field>
        <v-text-field label="Post Content" v-model="content"></v-text-field>
        <v-btn color="green" type="submit">Create New Post</v-btn>
    </v-form>
</template>

<script>
export default {
    name: "AddUser",
    data() {
        return {
            title: '',
            desc: '',
            content: ''
        }
    },
    methods: {
            onSubmit(e) {
                e.preventDefault();
                
                if(!this.title || !this.desc || !this.content) {
                    alert('Please add a text');
                    return
                }

                const newCard = {
                    // id: Math.floor(Math.random() * 100000),
                    title: this.title,
                    desc: this.desc,
                    content: this.content,
                }

                this.$emit('add-card', newCard);

                this.title = ''
                this.desc = ''
                this.content = ''
            }
        }
}
</script>