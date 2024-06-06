<template>
  <!-- 參考lao-jing老井 -->
  <section class="i-banner-wrap">
    <div class="i-banner__list swiper-wrapper">
      <!-- swiper-slide 改a標籤 則可整張圖設連結 -->
      <swiper class="swiper-slide"
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
      </swiper>
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
<script>
import { Swiper, SwiperSlide } from 'swiper/vue';
import { Autoplay, Pagination, Navigation } from 'swiper/modules';
import 'swiper/css';
import 'swiper/css/navigation';
import 'swiper/css/pagination';

export default {
  components: {
    Swiper,
    SwiperSlide,
  },
  data() {
    return {
      // 要使用的相依模組
      modules: [Autoplay, Navigation, Pagination],
    };
  },
};
</script>
