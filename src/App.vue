<template>
  <div>
    <search-bar @termChange="onTermChange"></search-bar>
    <video-list :videos="videos"></video-list>  
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar.vue";
import VideoList from "./components/VideoList.vue";

export default {
  name: "App",
  components: { SearchBar, VideoList },
  data() {
    return {
      videos: []
    };
  },
  methods: {
    async onTermChange(searchTerm) {
      const { data } = await axios.get(
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
      this.videos = data.items;
    }
  }
};
</script>