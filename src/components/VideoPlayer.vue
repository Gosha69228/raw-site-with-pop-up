<template>
  <div class="video-container">
    <video width="100%" height="100%" autoplay muted preload="auto">
      <source src="@/assets/privet.mp4" type="video/mp4" />
    </video>
  </div>
</template>


<script>
</script>

<style scoped>
.video-container {
  position: relative;
  padding-bottom: 56.25%; /* 16:9 соотношение сторон */
  overflow: hidden;
}

video {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>
