<template>
  <section class="i-banner swiper" ref="ibanRef">
    <div class="swiper-wrapper">
      <div class="swiper-slide"
      v-for="(item, index) in ibanslides" :key="index">
        <!-- 01 -->
        <template v-if="item.type === 'image'">
          <picture class="i-ban-pic">
            <!-- 輪播小圖尺寸 800x570 -->
            <source :srcset="item.source" media="(max-width: 991px)" />
            <!-- 輪播大圖尺寸 1920x850-->
            <img :src="item.src" class="img-fluid" alt="標題"
            width="1920" height="850" loading="lazy" />
          </picture>
          <div class="swiper-txt">
            <h2 class="headline" data-swiper-parallax="-400">
              {{ item.headline }}
            </h2>
            <p class="subtitle" data-swiper-parallax="-200">
              {{ item.subtitle }}
            </p>
            <a href="#" class="btn-banner" title="more detail">
              more detail <span></span></a>
          </div>
        </template>
        <!-- 02 Youtube影片
          data-plyr-embed-id：YouTube影片ID

          影片圖若不另傳照，可直接抓YT預設
          YT預設1280x720：//img.youtube.com/vi/${videoid}/maxresdefault.jpg
          YT預設640x480：//img.youtube.com/vi/${videoid}/sddefault.jpg
          -->
          <template v-else-if="item.type === 'video'">
            <picture class="i-ban-pic">
              <div class="video">
                <div class="js-player"
              data-plyr-provider="youtube" :data-plyr-embed-id="item.videoSrc"></div>
              <source :srcset="item.source" media="(max-width: 767px)">
              <img :src="item.src" alt="(圖)帶入名稱" width="1920" height="850">
              </div>
            </picture>
          </template>
      </div>
    </div>
    <div class="control-box control-style">
      <div class="swiper-button swiper-prev"></div>
      <div class="swiper-dots"></div>
      <div class="swiper-button swiper-next"></div>
    </div>
  </section>

</template>
<script setup>
import { onMounted, onUnmounted, ref } from 'vue';
import axios from 'axios';
import Swiper from 'swiper';
import { Autoplay, Pagination, Navigation } from 'swiper/modules';
import 'swiper/swiper-bundle.css';
import Plyr from 'plyr';
import 'plyr/dist/plyr.css';

// 安裝 Swiper 模組
Swiper.use([Autoplay, Pagination, Navigation]);

// json 資料
const ibanslides = ref();
const baseUrl = import.meta.env.VITE_API_BASE_URL;

// #01 methods swiper
const winH = ref(window.innerHeight);

const ibanRef = ref(null);
const kanbanT = ref(null);
const kanbanB = ref(null);
const ibanPlayers = ref([]);

const handleResize = () => {
  winH.value = window.innerHeight;
  if (ibanRef.value) {
    kanbanT.value = parseInt(ibanRef.value.getBoundingClientRect().top - winH.value * 0.5, 10);
    kanbanB.value = parseInt(ibanRef.value.offsetHeight + kanbanT.value + winH.value * 0.5, 10);
  }
};

const ibanSwiper = () => new Swiper(ibanRef.value, {
  slidesPerView: 1,
  loop: true,
  effect: 'fade',
  parallax: true,
  lazy: true,
  // autoplay: {
  //   delay: 5000,
  // },
  navigation: {
    nextEl: '.swiper-button.swiper-next',
    prevEl: '.swiper-button.swiper-prev',
  },
  pagination: {
    el: ibanRef.value.querySelector('.swiper-dots'),
    clickable: true,
    type: 'fraction',
    formatFractionCurrent(number) {
      return (`0${number}`).slice(-2);
    },
    formatFractionTotal(number) {
      return (`0${number}`).slice(-2);
    },
    renderFraction(currentClass, totalClass) {
      return `<span class="${currentClass}"></span>
      <span class="gap">/</span>
      <span class="${totalClass}"></span>`;
    },
  },
  on: {
    resize: () => {
      handleResize();
    },
    init: (swiper) => {
      // 初始化 Plyr 播放器
      const players = Array.from(ibanRef.value.querySelectorAll('.js-player')).map((p) => new Plyr(p, {
        muted: true,
        hideControls: true,
      }));

      ibanPlayers.value = players;

      players.forEach((player, index) => {
        player.on('ready', () => {
          if (index === 0 && player.elements.settingsContainer.closest('.swiper-slide-active')) {
            player.play();
          }
        });
        player.on('playing', () => {
          ibanRef.value.classList.add('is-video-playing');
          swiper.autoplay.stop();
        });
        player.on('pause', () => {
          ibanRef.value.classList.remove('is-video-playing');
        });
        player.on('ended', () => {
          swiper.autoplay.start();
          swiper.slideNext(800);
        });
      });
    },
    slideChangeTransitionStart: (swiper) => {
      const prevSlide = swiper.slides[swiper.previousIndex];

      const prevVideo = ibanPlayers.value.find((player) => player.id === prevSlide.querySelector('.js-player').id);
      if (prevVideo && prevVideo.playing) {
        prevVideo.pause();
      }
    },
    slideChangeTransitionEnd: (swiper) => {
      const currentSlide = swiper.slides[swiper.activeIndex];

      const currentVideo = ibanPlayers.value.find((player) => player.id === currentSlide.querySelector('.js-player').id);
      if (currentVideo && !currentVideo.playing) {
        currentVideo.play();
      }
    },
  },
});

onMounted(() => {
  axios.get(`${baseUrl}/iban.json`)
    .then((response) => {
      ibanslides.value = response.data;
    })
    .catch((error) => {
      console.error('Error fetching data:', error);
    });

  ibanSwiper();

  // 監聽窗口大小變化
  window.addEventListener('resize', handleResize);
});

onUnmounted(() => {
  window.removeEventListener('resize', handleResize);
});

</script>
