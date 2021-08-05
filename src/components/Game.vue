<template>
  <div class="bg-img">
    <h1>{{ game }}</h1>
    <h2>Game Series</h2>
    <div class="char-list-wrapper">
      <div v-for="(char, index) in games" :key="index">
        <router-link
          :to="'/character-lineup/' + char.head + char.tail"
          class="char-list"
        >
          <div class="char-list-img-wrapper">
            <img :src="char.image" />
          </div>
          <span>{{ char.character }}</span>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      game: this.$route.params.game,
      games: []
    };
  },
  mounted() {
    this.$http
      .get("https://www.amiiboapi.com/api/amiibo/?gameseries=" + this.game)
      .then((response) => (this.games = response.data.amiibo));
  }
};
</script>
