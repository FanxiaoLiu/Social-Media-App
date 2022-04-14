<template>
    <v-app>
        <Cards :cards="cards" />
    </v-app>
</template>

<script>
import Cards from '../components/Cards'


export default {
  name: 'App',

  data() {
    return {
      cards: []
    }
  },
  components: {
    Cards,
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
    async deleteCards(id) {
      if (confirm('Are you sure?')) {
        const res = await fetch(`api/cards/${id}`, {
          method: 'DELETE'
        })

        res.status === 200 ? (this.cards = this.cards.filter((card) => card.id !== id)) : alert('Error deleting task')

      }
    },
    async fetchCards() {
      const res = await fetch('api/cards')
      const data = await res.json()

      return data
    },
    async fetchCard(id) {
      const res = await fetch(`api/cards/${id}`)
      const data = await res.json()

      return data
    },
  },
  async created() {
    this.cards = await this.fetchCards();
  }
}
</script>

