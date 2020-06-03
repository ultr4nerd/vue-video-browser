<template>
  <div>
    <SearchBar @termChange="onTermChange"></SearchBar>
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar.vue";
export default {
  name: "App",
  components: { SearchBar },
  methods: {
    async onTermChange(searchTerm) {
      const response = await axios.get(
        "https://www.googleapis.com/youtube/v3/search",
        {
          params: {
            key: process.env.VUE_APP_YOUTUBE_API_KEY,
            type: "video",
            part: "snippet",
            q: searchTerm
          }
        }
      );
      console.log(response);
    }
  }
};
</script>