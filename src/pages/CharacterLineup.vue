<template>
  <div class="bg-img">
    <h1>Character Lineup</h1>
    <div v-if="isLoading" class="spinner-wrapper">
      <img
        src="../assets/spinner.gif"
        alt="Loading..."
        class="loading-spinner"
      />
    </div>
    <div class="char-list-wrapper">
      <div v-for="(char, index) in chars" :key="index">
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
      isLoading: false,
      chars: []
    };
  },
  mounted() {
    this.isLoading = true;
    const uri = "https://www.amiiboapi.com/api/amiibo";
    this.$http
      .get(uri)
      .then((response) => (this.chars = response.data.amiibo))
      .finally(() => {
        this.isLoading = false;
      });
  }
};
</script>
