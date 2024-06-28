<template>
  <div class="popup" v-if="showPopup">
    <div class="popup-content">
      <div class="video-container">
        <video :src="currentVideoUrl" width="1120" height="630" autoplay @loadedmetadata="videoLoaded"
          @ended="videoEnded"></video>
      </div>
      <div class="controls">
        <transition-group name="fade-in-button" mode="out-in">
          <button v-for="(button, index) in videoButtons[currentVideoId]" :key="button.videoId"
            @click="changeVideo(button.videoId)"
            :class="{ 'hidden': !button.visible, 'popup-button': button.visible, 'bounce-enter-active': button.visible }">
            {{ button.label }}
          </button>
        </transition-group>
        <button @click="closePopup">Закрыть</button>
      </div>
    </div>
  </div>
</template>


<script>

import privetVideo from "@/assets/privet.mp4";
import sbotomVideo from "@/assets/sbotom.mp4";
import oviplateVideo from "@/assets/oviplate.mp4";
import tovarnepodVideo from "@/assets/tovarnepod.mp4";
import zachemVideo from "@/assets/zachem.mp4";
import kakie_tovariVideo from "@/assets/kakie_tovari.mp4";
import kakvse_ustVideo from "@/assets/kakvse_ust.mp4";
import trebovanieotzivVideo from "@/assets/trebovanieotziv.mp4";
import uze_smotrelVideo from "@/assets/uze_smotrel.mp4";
import pervi_rasVideo from "@/assets/pervi_ras.mp4";

export default {
  props: {
    showPopup: Boolean,
    currentVideoId: String,
  },
  emits: ['change-video', 'toggle-sound', 'close-popup'],
  computed: {
    currentVideoUrl() {
      if (this.currentVideoId === 'privet') {
        return privetVideo;
      } else if (this.currentVideoId === 'oviplate') {
        return oviplateVideo;
      } else if (this.currentVideoId === 'sbotom') {
        return sbotomVideo;
      } else if (this.currentVideoId === 'tovarnepod') {
        return tovarnepodVideo;
      } else if (this.currentVideoId === 'zachem') {
        return zachemVideo;
      } else if (this.currentVideoId === 'kakie_tovari') {
        return kakie_tovariVideo;
      } else if (this.currentVideoId === 'kakvse_ust') {
        return kakvse_ustVideo;
      } else if (this.currentVideoId === 'trebovanieotziv') {
        return trebovanieotzivVideo;
      } else if (this.currentVideoId === 'uze_smotrel') {
        return uze_smotrelVideo;
      } else if (this.currentVideoId === 'pervi_ras') {
        return pervi_rasVideo;
      } else {
        return '';
      }
    },

  },
  data() {
    return {
      buttonIndex: 0, // Индекс текущей кнопки
      isFirstTimeWatching: true,
      videoWatchCount: 0,
      videoButtons: {
        'privet': [
          // Набор кнопок для "Приветствие"
          { videoId: 'zachem', label: 'Зачем это нужно магазину', delay: 3000 },
          { videoId: 'kakvse_ust', label: 'Как всё устроено', delay: 6000 },
        ],
        'kakvse_ust': [
          // Набор кнопок для "Как всё устроено"
          { videoId: 'zachem', label: 'Зачем это нужно магазину', delay: 2000 },
          { videoId: 'sbotom', label: 'Как взаимодействовать с ботом', delay: 4000 },
          { videoId: 'kakie_tovari', label: 'Какие товары есть', delay: 6000 },
          { videoId: 'oviplate', label: 'О выплате', delay: 8000 },
          { videoId: 'trebovanieotziv', label: 'Требование к отзыву', delay: 9000 },
          { videoId: 'kakvse_ust', label: 'ЗАМЕНИТЬ НА БОТА', delay: 10000 },
        ],
        'zachem': [
          // Набор кнопок для "Зачем это нужно магазину"
          { videoId: 'kakvse_ust', label: 'Как все устроено', delay: 3000 },
          { videoId: 'kakie_tovari', label: 'Какие товары есть', delay: 6000 },
          { videoId: 'oviplate', label: 'О выплате', delay: 8000 },
          { videoId: 'zachem', label: 'ЗАМЕНИТЬ НА БОТА', delay: 10000 },
        ],
        'sbotom': [
          // Набор кнопок для "Как взаимодействовать с ботом"
          { videoId: 'kakie_tovari', label: 'Какие товары есть', delay: 1500 },
          { videoId: 'trebovanieotziv', label: 'Требование к отзыву', delay: 3000 },
          { videoId: 'oviplate', label: 'О выплате', delay: 5000 },
          { videoId: 'tovarnepod', label: 'Если не подойдет товар', delay: 6000 },
          { videoId: 'sbotom', label: 'ЗАМЕНИТЬ НА БОТА', delay: 8000 },
        ],
        'kakie_tovari': [
          // Набор кнопок для "Какие товары есть"
          { videoId: 'oviplate', label: 'О выплате', delay: 3000 },
          { videoId: 'kakie_tovari', label: 'ЗАМЕНИТЬ НА БОТА', delay: 6000 },
        ],
        'oviplate': [
          // Набор кнопок для "О выплате"
          { videoId: 'kakie_tovari', label: 'Какие товары есть', delay: 3000 },
          { videoId: 'oviplate', label: 'ЗАМЕНИТЬ НА БОТА', delay: 6000 },
        ],
        'tovarnepod': [
          // Набор кнопок для "Если не подойдет товар"
          { videoId: 'kakie_tovari', label: 'Какие товары есть', delay: 3000 },
          { videoId: 'trebovanieotziv', label: 'Требование к отзыву', delay: 6000 },
          { videoId: 'tovarnepod', label: 'ЗАМЕНИТЬ НА БОТА', delay: 9000 },
        ],
        'trebovanieotziv': [
          // Набор кнопок для "Требование к отзыву"
          { videoId: 'kakie_tovari', label: 'Какие товары есть', delay: 3000 },
          { videoId: 'trebovanieotziv', label: 'ЗАМЕНИТЬ НА БОТА', delay: 6000 },
        ],
        'pervi_ras': [
          // Набор кнопок для "Первый раз смотрит"
          { videoId: 'kakie_tovari', label: 'Какие товары есть', delay: 2000 },
          { videoId: 'trebovanieotziv', label: 'Требование к отзыву', delay: 4000 },
          { videoId: 'oviplate', label: 'О выплате', delay: 6000 },
          { videoId: 'tovarnepod', label: 'Если не подойдет товар', delay: 8000 },
          { videoId: 'pervi_ras', label: 'ЗАМЕНИТЬ НА БОТА', delay: 10000 },
        ],
        'uze_smotrel': [
          // Набор кнопок для "Уже смотрел завершение"
          { videoId: 'kakie_tovari', label: 'Какие товары есть', delay: 2000 },
          { videoId: 'trebovanieotziv', label: 'Требование к отзыву', delay: 4000 },
          { videoId: 'oviplate', label: 'О выплате', delay: 6000 },
          { videoId: 'tovarnepod', label: 'Если не подойдет товар', delay: 8000 },
          { videoId: 'uze_smotrel', label: 'ЗАМЕНИТЬ НА БОТА', delay: 9000 },
        ],
      },
    };
  },
  methods: {
    changeVideo(videoId) {
      if (this.isFirstTimeWatching) {
        this.$emit('change-video', videoId);
      }
    },
    closePopup() {
      this.$emit('close-popup');
    },
    videoLoaded() {
      const buttons = this.videoButtons[this.currentVideoId];
      buttons.forEach((button, index) => {
        setTimeout(() => {
          button.visible = true;
        }, button.delay);
      });
    },
    videoEnded() {
      // Проверяем, не является ли текущее видео "первый раз смотрит" или "уже смотрел завершение"
      if (this.currentVideoId !== 'pervi_ras' && this.currentVideoId !== 'uze_smotrel') {
        // Проверяем Local Storage для определения, смотрит ли пользователь текущее видео впервые
        const firstTimeWatching = localStorage.getItem(this.currentVideoId) !== "false";
        if (firstTimeWatching) {
          // Запускаем блок "первый раз смотрит"
          setTimeout(() => {
            this.changeVideo('pervi_ras');
          }, 5000);
          // Устанавливаем состояние Local Storage, чтобы показать, что первый просмотр завершен
          localStorage.setItem(this.currentVideoId, "false");
        } else {
          // Запускаем блок "уже смотрел завершение"
          setTimeout(() => {
            this.changeVideo('uze_smotrel');
          }, 5000);
        }
      }
    },
  },
};
</script>

<style scoped>
/* Стили для поп-апа и его элементов */
.popup {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 999;
}

.popup-content {
  background-color: rgb(225, 225, 219);
  padding: 20px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
  text-align: center;
  width: 1160px;
}

.video-container {
  margin-bottom: 20px;
}

/* Стили для видео-контейнера, если это необходимо */
.controls button {
  margin-right: 10px;
  padding: 15px 30px;
  border-radius: 10px;
  background-color: inherit;
  color: #000;
  font-size: 16px;
  cursor: pointer;
}

.controls button:last-child {
  margin-right: 0;
}

.hidden {
  display: none;
}

.bounce-enter-active {
  animation: bounce-in 0.5s;
}


@keyframes bounce-in {
  0% {
    transform: scale(0);
  }

  50% {
    transform: scale(1.25);
  }

  100% {
    transform: scale(1);
  }
}
</style>
