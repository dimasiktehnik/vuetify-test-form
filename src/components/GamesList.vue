<template>
  <v-dialog
      v-model="dialog"
      width="500"
  >
    <template v-slot:activator="{ on, attrs }">
      <v-card elevation="11">
        <v-card-title><h1>Play Chess</h1></v-card-title>
        <v-card-text>
          <v-list>
            <v-list-item-group v-model="selectedGame" mandatory>
              <Game
                  v-for="(game,index) in games"
                  :key="index"
                  :game="game"
                  :id="index"
                  @removeItem="removeGame"
              />
            </v-list-item-group>
          </v-list>
          <v-btn
              dark
               v-bind="attrs"
               v-on="on">
            New game
          </v-btn>
        </v-card-text>
      </v-card>
    </template>
    <v-card>
      <v-card-title class="headline grey lighten-2">
        New game
      </v-card-title>
      <v-card-text>
        <v-text-field v-model="name" label="Name of game"/>
        <v-text-field v-model="image" label="Image url"/>
      </v-card-text>
      <v-card-actions class="justify-center">
        <v-btn
            color="primary"
            text
            @click="saveGame(name, image)"
        >
          Create
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
import Game from "@/components/Game";

export default {
  components: { Game },
  watch: {
    selectedGame () {
      this.$emit('selectedGame', this.games[this.selectedGame]);
    }
  },
  data() {
    return {
      dialog: false,
      selectedGame: 0,
      games: [],
      name: '',
      image: ''
    }
  },
  mounted() {
    if (localStorage.games) {
      this.games = JSON.parse(localStorage.getItem('games'));
    }
    this.$emit('selectedGame', this.games[this.selectedGame]);
  },
  methods: {
    saveGame(name, image) {
      if(name.length === 0){
        return
      }
      this.dialog = false;
      this.games.push({name, image});
      this.name = '';
      this.image = '';
      localStorage.setItem('games', JSON.stringify(this.games));
      this.$emit('selectedGame', this.games[this.selectedGame]);
    },
    removeGame(id) {
      this.games.splice(id, 1);
      localStorage.setItem('games', JSON.stringify(this.games));
    }
  }
}

</script>