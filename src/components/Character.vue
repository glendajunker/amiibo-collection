<template>
  <div>
    <div class="single-char bg-img">
      <img :src="character.image" />
      <div class="single-char-info">
        <h1>{{ character.name }}</h1>
        <p>Series: {{ character.amiiboSeries }}</p>
        <p>Character: {{ character.character }}</p>
        <p>Game Series: {{ character.gameSeries }}</p>
        <p>Type: {{ character.type }}</p>
      </div>
    </div>
    <div class="related">
      <h3>More from {{ character.amiiboSeries }} series</h3>
      <div class="char-list-wrapper">
        <div v-for="(char, index) in seriesCharList" :key="index">
          <router-link
            :to="'/character-lineup/' + char.head + char.tail"
            class="char-list"
          >
            <div class="char-list-img-wrapper">
              <img :src="char.image" />
            </div>
            <span>{{ char.name }}</span>
          </router-link>
        </div>
      </div>
      <router-link
        :to="'/browse-series/' + this.characterSeries"
        class="view-more"
        >View More ></router-link
      >
      <br />
      <br />
      <hr />
    </div>

    <div class="related">
      <h3>More from {{ character.gameSeries }} game series</h3>
      <div class="char-list-wrapper">
        <div v-for="(char, index) in gameSeriesCharList" :key="index">
          <router-link
            :to="'/character-lineup/' + char.head + char.tail"
            class="char-list"
          >
            <div class="char-list-img-wrapper">
              <img :src="char.image" />
            </div>
            <span>{{ char.name }}</span>
          </router-link>
        </div>
      </div>
      <router-link
        :to="'/browse-games/' + this.characterGameSeries"
        class="view-more"
        >View More ></router-link
      >
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      id: this.$route.params.id,
      character: {},
      characterSeries: "",
      characterGameSeries: "",
      seriesCharList: [],
      gameSeriesCharList: []
    };
  },
  created() {
    this.$http
      .get("https://www.amiiboapi.com/api/amiibo/?id=" + this.id)
      .then((response) => {
        this.character = response.data.amiibo;
        this.characterGameSeries = this.character.gameSeries;
        this.characterSeries = this.character.amiiboSeries;
      })
      .then(() => {
        this.$http
          .get(
            "https://www.amiiboapi.com/api/amiibo/?gameseries=" +
              this.characterGameSeries
          )
          .then((response) => {
            let shuffledArray = response.data.amiibo.sort(
              () => Math.random() - 0.5
            );
            this.gameSeriesCharList = shuffledArray.slice(0, 3);
          });
      })
      .then(() => {
        this.$http
          .get(
            "https://www.amiiboapi.com/api/amiibo/?amiiboSeries=" +
              this.characterSeries
          )
          .then((response) => {
            console.log(response);
            let shuffledArray = response.data.amiibo.sort(
              () => Math.random() - 0.5
            );
            this.seriesCharList = shuffledArray.slice(0, 3);
          });
      });
  },
  watch: {
    $route(to, from) {
      if (to !== from) {
        location.reload();
      }
    }
  }
};
</script>

<style scoped>
h1 {
  text-align: left;
}
.single-char {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  align-items: center;
  padding: 3em 0;
  border-bottom: 8px solid lightgrey;
}

.single-char img {
  max-width: 300px;
  max-height: 300px;
  padding: 0 2em;
}

.single-char-info {
  padding: 0 2em;
  font-size: 0.9em;
  line-height: 1.2em;
}

.single-char-info h1 {
  margin-bottom: 1em;
}

.related {
  margin: 3em auto;
  width: 80%;
}
</style>
