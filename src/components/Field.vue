<template>
  <div v-if="selectedGame">
    <v-checkbox
        v-model="checkedPlayers"
        value="player1"
        :label="`Player 1:`"
    />
    <v-img
        v-if="selectedGame.image"
        max-height="250"
        max-width="250"
        :src="selectedGame.image"
    />
    <v-img
        v-else
        max-height="250"
        max-width="250"
        src="https://piotrkowalski.pw/assets/camaleon_cms/image-not-found-4a963b95bf081c3ea02923dceaeb3f8085e1a654fc54840aac61a57a60903fef.png"
    />
    <v-checkbox
        v-model="checkedPlayers"
        value="player2"
        :label="`Player 2:`"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      checkedPlayers: []
    }
  },
  props: {
    selectedGame: {
      type: Object,
      default: () => {}
    }
  }
}
</script>