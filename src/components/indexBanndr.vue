<template>
  <!-- 參考lao-jing老井 -->
  <section class="i-banner-wrap">
    <div class="swiper-wrapper">
      <!-- swiper-slide 改a標籤 則可整張圖設連結 -->
      <div class="swiper-slide">
        <div class="item">
          <picture class="background">
            <source srcset="assets/images/del/ban1s.jpg" media="(max-width: 743px)">
            <img src="assets/images/del/ban1.jpg" alt="(圖)" width="1920" height="975">
          </picture>
        </div>
      </div>
      <!-- @ YouTube -->
      <div class="swiper-slide">
        <div class="item">
          <div class="js-player"
          data-plyr-provider="youtube" data-plyr-embed-id="usf_4ur5V2Y"></div>
        </div>
      </div>
    </div>
    <!-- dot -->
    <div class="control-box">
      <div class="swiper-dots"></div>
    </div>
    <div class="scrolldown">SCROLL</div>
  </section>
</template>
<script setup>

</script>
