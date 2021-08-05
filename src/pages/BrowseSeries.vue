<template>
  <div class="bg-img">
    <h1>Browse by Series</h1>
    <div v-if="isLoading" class="spinner-wrapper">
      <img
        src="../assets/spinner.gif"
        alt="Loading..."
        class="loading-spinner"
      />
    </div>
    <div class="browse-by-wrapper">
      <div v-for="(serie, index) in series" :key="index" class="browse-by-item">
        <router-link :to="'/browse-series/' + serie">
          <p>{{ serie }}</p>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isLoading: false,
      chars: [],
      series: []
    };
  },
  mounted() {
    this.isLoading = true;
    const uri = "https://www.amiiboapi.com/api/amiibo";
    this.$http
      .get(uri)
      .then((response) => {
        this.chars = response.data.amiibo;
        this.chars.forEach((char) => {
          if (!this.series.includes(char.amiiboSeries))
            this.series.push(char.amiiboSeries);
        });
      })
      .finally(() => {
        this.isLoading = false;
      });
  }
};
</script>
