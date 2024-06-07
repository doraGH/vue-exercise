<template>
  <section class="i-banner swiper">
    <div class="swiper-wrapper">
      <a href="#" class="swiper-slide" title="查看更多"
      v-for="(item, index) in ibanslides" :key="index">
        <picture>
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
      </a>
    </div>
    <div class="control-box">
      <div class="swiper-pagination"></div>
      <div class="swiper-button-prev"></div>
      <div class="swiper-button-next"></div>
      <div class="autoplay-progress">
        <svg viewBox="0 0 30 30">
          <circle cx="15" cy="15" r="13"></circle>
        </svg>
        <span></span>
      </div>
    </div>
  </section>

  <section class="i-banner-wrap">
    <div class="i-banner__list swiper-wrapper">
      <!-- swiper-slide 改a標籤 則可整張圖設連結 -->
      <div class="swiper-slide"
      :slides-per-view="1"
      :space-between="0"
      :modules="modules"
      :loop="true"
      :autoplay="{
        delay: 5000,
        disableOnInteraction: false,
      }"
      :navigation="true"
      :pagination="{ clickable: true }"
      >
        <swiper-slide class="item">
          <div class="foreground">
            <img src="../assets/images/del/ban4_txt.png" alt="(圖)">
          </div>
          <picture class="background">
            <source srcset="../assets/images/del/ban1s.jpg" media="(max-width: 743px)">
            <img src="../assets/images/del/ban1.jpg" alt="(圖)" width="1920" height="975">
          </picture>
        </swiper-slide>
      </div>
      <!-- @ YouTube -->
      <!-- <div class="swiper-slide">
        <div class="item">
          <div class="js-player"
          data-plyr-provider="youtube" data-plyr-embed-id="usf_4ur5V2Y"></div>
        </div>
      </div> -->
    </div>
    <!-- dot -->
    <!-- <div class="control-box">
      <div class="swiper-dots"></div>
    </div> -->
    <!-- <div class="swiper-button-prev"></div>
    <div class="swiper-button-next"></div>
    <div class="swiper-pagination"></div> -->
    <div class="scrolldown"></div>
  </section>
</template>
<script setup>
import { onMounted, ref } from 'vue';
import Swiper from 'swiper';
import { Autoplay, Pagination, Navigation } from 'swiper/modules';
import 'swiper/swiper-bundle.css';

// 安裝 Swiper 模組
Swiper.use([Autoplay, Pagination, Navigation]);

// json
const ibanslides = ref([
  {
    source: 'https://images.unsplash.com/photo-1547891654-e66ed7ebb968?q=80&w=900&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
    src: 'https://images.unsplash.com/photo-1547891654-e66ed7ebb968?q=80&w=1280&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
    headline: 'Quality First',
    subtitle: 'he leading equipment company in Asia for the design, development, and manufacturing of circuit board dust cleaning machines and consumables.',
  },
  {
    source: 'https://images.unsplash.com/photo-1578301978018-3005759f48f7?q=80&w=960&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
    src: 'https://images.unsplash.com/photo-1578301978018-3005759f48f7?q=80&w=1280&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
    headline: 'Two two',
    subtitle: 'he leading equipment company in Asia for the design, development.',
  },
]);

// methods
const ibanSwiper = () => new Swiper('.i-banner', {
  slidesPerView: 1,
  loop: true,
  effect: 'fade',
  parallax: true,
  lazy: true,
  autoplay: {
    delay: 5000,
  },
  pagination: {
    el: '.swiper-pagination',
    clickable: true,
  },
});

onMounted(() => {
  ibanSwiper();
});

</script>
