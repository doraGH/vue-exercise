<template>
  <header class="header">
    <div class="w-container">
      <a href="#" class="logo">
        <img src="../assets/images/logo.svg" />
        <span>Your Company</span>
      </a>

      <!-- Navigation Switch -->
      <a href="#navigation" class="nav-switch" title="點擊前往主導覽"
      :class="{'is-open': isOpen}" @click="isOpen = !isOpen">
        <span></span>
        <span></span>
        <span></span>
      </a>

      <!-- Navigation -->
      <nav id="navigation" class="nav">
        <ul class="menu reset">
          <li>
            <a href="#" title="關於本區">關於本區</a>
          </li>
          <li>
            <a href="#" title="最新消息">最新消息</a>
            <ul>
              <li><a href="#" title="最新公告">最新公告</a></li>
              <li><a href="#" title="活動資訊">活動資訊</a></li>
            </ul>
          </li>
        </ul>
      </nav>

    </div>
  </header>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import MobileDetect from 'mobile-detect';

onMounted(() => {
  // Mobile Detect
  const UA = window.navigator.userAgent;
  const md = new MobileDetect(UA);
  const { body } = document;
  if (md.mobile()) {
    body.classList.add('mb');
  } else {
    body.classList.add('pc');
  }
});

const isOpen = ref(false);

</script>
<style lang="scss" scoped>

</style>
