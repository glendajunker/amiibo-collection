<template>
  <div class="home-header bg-img">
    <div class="home-header-wrapper">
      <h1>{{ title }}</h1>
      <input
        v-model="filter"
        id="home-search-input"
        type="text"
        placeholder="Search character, game, series..."
      />
      <div class="char-list-wrapper">
        <div v-for="(char, index) in filteredChars" :key="index">
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
      <div class="home-nav-img-wrapper">
        <router-link to="/character-lineup" class="home-nav-img">
          <img src="../assets/character-lineup.jpg" alt="character lineup" />
          <span>Character Lineup</span>
        </router-link>
        <router-link to="/browse-games" class="home-nav-img">
          <img src="../assets/browse-by-game.jpg" alt="character lineup" />
          <span>Browse by Game</span>
        </router-link>
        <router-link to="/browse-series" class="home-nav-img">
          <img src="../assets/browse-by-series.jpg" alt="character lineup" />
          <span>Browse by Series</span>
        </router-link>
      </div>
    </div>
    <img src="../assets/home-footer.png" alt="" class="home-footer-img" />
  </div>
</template>
<script>
export default {
  data() {
    return {
      title: "Browse amiibo and create your own collection!",
      chars: [],
      filter: ""
    };
  },
  computed: {
    filteredChars() {
      if (this.filter === "") return;
      return this.chars.filter((char) => {
        let searchTerm = this.filter.toLowerCase();
        return (
          char.amiiboSeries.toLowerCase().includes(searchTerm) ||
          char.character.toLowerCase().includes(searchTerm) ||
          char.gameSeries.toLowerCase().includes(searchTerm) ||
          char.name.toLowerCase().includes(searchTerm)
        );
      });
    }
  },
  mounted() {
    this.$http
      .get("https://www.amiiboapi.com/api/amiibo")
      .then((response) => (this.chars = response.data.amiibo));
  }
};
</script>

<style scoped>
.home-header {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
}

.home-header-wrapper {
  min-height: 100%;
  padding: 0 2em;
  display: flex;
  align-items: center;
  flex-direction: column;
}

h1 {
  font-size: 1.5em;
  max-width: 350px;
}

#home-search-input {
  margin-top: 2em;
  padding: 0.7em 1.7em;
  border-radius: 40px;
  border: 1px solid #848484;
  box-sizing: border-box;
  max-width: 400px;
  width: 95%;
  font-size: 1em;
}

#home-search-input:focus {
  border: 1px solid #000;
  outline: none;
}

#home-search-input:hover {
  border: 1px solid #000;
}

.home-nav-img-wrapper {
  margin-bottom: 3em;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.home-nav-img {
  display: flex;
  flex-direction: column;
  padding: 1.5em;
  text-align: center;
}

.home-nav-img img {
  border-radius: 15px;
}

.home-nav-img span {
  margin-top: 1em;
  font-weight: bold;
  text-align: center;
  text-transform: uppercase;
}

.home-footer-img {
  width: 75%;
  max-width: 980px;
}
</style>
