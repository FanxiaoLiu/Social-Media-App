<template>
  <v-app>
    <AddCard @add-card="addCard" />
  </v-app>
</template>

<script>
import AddCard from "../components/AddCard"

export default {
  name: "AboutView",
  components: {
    AddCard
  },
  data() {
    return {
      cards: [],
    }
  },
  methods: {
    async addCard(card) {
      const res = await fetch('api/cards', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(card),
      })

      const data = await res.json() 

      this.cards = [...this.cards, data]
    },
    async fetchCards() {
      const res = await fetch('api/cards')
      const data = await res.json()

      return data
    },
  },
  async created() {
    this.cards = await this.fetchCards();
  }
}
</script>