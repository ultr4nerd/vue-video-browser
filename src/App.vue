<template>
  <div class="container">
    <search-bar @termChange="onTermChange"></search-bar>
    <div class="row">
      <video-detail :video="selectedVideo" />
      <video-list :videos="videos" @videoSelect="onVideoSelect" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar.vue";
import VideoList from "./components/VideoList.vue";
import VideoDetail from "./components/VideoDetail.vue";

export default {
  name: "App",
  components: { SearchBar, VideoList, VideoDetail },
  data() {
    return { videos: [], selectedVideo: null };
  },
  methods: {
    onVideoSelect(video) {
      this.selectedVideo = video;
    },
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