<template>
  <v-list-item>
    <span>{{game.name}}</span>
    <span class="pipe">|</span>
    <span class="archive" @click="archive()">Archive</span>
  </v-list-item>
</template>

<script>
export default {
  props: {
    game: {
      type: Object,
      default: () => {
      }
    },
    id: {
      type: Number,
      default: 0
    }
  },
  methods: {
    archive() {
      this.$emit('removeItem', this.id);
    }
  }
}
</script>

<style>
.pipe {
  margin: 10px;
}
.archive {
  text-decoration: underline;
  color: blue;
}
</style>