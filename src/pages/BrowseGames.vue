<template>
  <div class="bg-img">
    <h1>Browse by Game</h1>
    <div v-if="isLoading" class="spinner-wrapper">
      <img
        src="../assets/spinner.gif"
        alt="Loading..."
        class="loading-spinner"
      />
    </div>
    <div v-if="error">
      <pre>{{ error }}</pre>
    </div>
    <div class="browse-by-wrapper" v-if="games">
      <div v-for="(game, index) in games" :key="index" class="browse-by-item">
        <router-link :to="'/browse-games/' + game">
          <p>{{ game }}</p>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import api from "@/services/api";

export default {
  data() {
    return {
      isLoading: false,
      error: null,
      games: null
    };
  },
  mounted() {
    this.isLoading = true;
    api
      .getGames()
      .then(
        (response) => {
          this.games = new Set(
            response.amiibo.map(({ gameSeries }) => gameSeries)
          );
        },
        (error) => {
          this.error = error;
        }
      )
      .finally(() => {
        this.isLoading = false;
      });
  }
};
</script>
