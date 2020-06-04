<template>
  <ul>
    <video-list-item v-for="video in videos" :key="video.etag" :video="video" />
  </ul>
</template>

<script>
import VideoListItem from "./VideoListItem.vue";

export default {
  name: "VideoList",
  components: { VideoListItem },
  props: {
    videos: Array
  }
};
</script>
