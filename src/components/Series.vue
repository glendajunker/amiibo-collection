<template>
  <div class="bg-img">
    <h1>{{ serie }}</h1>
    <h2>Series</h2>
    <div class="char-list-wrapper">
      <div v-for="(char, index) in series" :key="index">
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
      serie: this.$route.params.serie,
      series: []
    };
  },
  mounted() {
    this.$http
      .get("https://www.amiiboapi.com/api/amiibo/?amiiboSeries=" + this.serie)
      .then((response) => (this.series = response.data.amiibo));
  }
};
</script>
