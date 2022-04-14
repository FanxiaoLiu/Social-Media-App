<template>
    <v-app-bar
      color="deep-purple accent-4"
      dark
      prominent
    >

      <v-toolbar-title>My files</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-filter</v-icon>
      </v-btn>

      <v-btn icon>
        <router-link to="/"><v-icon>mdi-home</v-icon></router-link>
      </v-btn>

      <v-btn icon>
        <router-link to="/about"><v-icon>mdi-file</v-icon></router-link>
      </v-btn>
    </v-app-bar>
</template>

<script>
export default {
    name: "NavBar",
}
</script>