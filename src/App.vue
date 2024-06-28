<template>
  <div>
    <h2>это может каждый</h2>
    <h1 class="custom-heading">
      ПОЛУЧАЙТЕ ТОВАРЫ НА МАРКЕТПЛЕЙСАХ БЕСПЛАТНО
    </h1>
    <VideoPlayer />
    <Popup
      :showPopup="showPopup"
      :currentVideoId="currentVideoId"
      @change-video="changeVideo"
      @close-popup="closePopup"
    />
    <button @click="openPopup">Открыть поп-ап</button>
  </div>
</template>

<script>
import VideoPlayer from "./components/VideoPlayer.vue";
import Popup from "./components/Popup.vue";


export default {
  components: {
    VideoPlayer,
    Popup,
  },
  data() {
    return {
      showPopup: false,
      currentVideoId: "privet", // Идентификатор начального видео
    };
  },
  methods: {
    openPopup() {
      this.showPopup = true;
    },
    changeVideo(videoId) {
      this.currentVideoId = videoId; // Обновляем идентификатор видео
    },
    closePopup() {
      this.showPopup = false;
    },
  },
};
</script>

<style scoped>
.custom-heading {
  font-size: 48px;
  text-align: left;
  line-height: 1.2;
}
</style>
