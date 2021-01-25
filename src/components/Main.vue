<template>
    <v-container fill-height>
      <div class="theme-button">
        <v-tooltip v-if="!$vuetify.theme.dark"
                   bottom>
          <template v-slot:activator="{ on }">
            <v-btn v-on="on"
                   color="info"
                   small
                   fab
                   @click="darkMode">
              <v-icon class="mr-1">mdi-moon-waxing-crescent</v-icon>
            </v-btn>
          </template>
          <span>Dark Mode On</span>
        </v-tooltip>

        <v-tooltip v-else
                   bottom>
          <template v-slot:activator="{ on }">
            <v-btn v-on="on"
                   color="info"
                   small
                   fab
                   @click="darkMode">
              <v-icon color="yellow">mdi-white-balance-sunny</v-icon>
            </v-btn>
          </template>
          <span>Dark Mode Off</span>
        </v-tooltip>
      </div>
      <v-row align="center"
             justify="center">
        <v-col>
          <Field :selectedGame="selectedGame"/>
        </v-col>
        <v-col>
          <GamesList @selectedGame="setSelectedGame"/>
        </v-col>
      </v-row>
    </v-container>
</template>

<style>
.theme-button {
  position: absolute;
  top: 40px;
  right: 30px;
}
</style>

<script>
import Field from "@/components/Field";
import GamesList from "@/components/GamesList";

export default {
  components: {
    GamesList,
    Field,
  },
  data() {
    return {
      selectedGame: {}
    }
  },
  methods: {
    setSelectedGame(game) {
      this.selectedGame = game;
    },
    darkMode() {
      this.$vuetify.theme.dark = !this.$vuetify.theme.dark;
    }
  }
};
</script>

