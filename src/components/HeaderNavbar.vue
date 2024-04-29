<template>
  <header class="header">
    <div class="w-container" :class="{'is-open-nav': isOpen}">
      <a href="#" class="nav-brand">
        <img src="../assets/images/logo.svg" />
        <span>Your Company</span>
      </a>

      <!-- Navigation -->
      <nav class="navbar">
        <ul class="menu">
          <li>
            <a href="#" title="關於本區">關於本區</a>
          </li>
          <li class="has-child" :class="{'is-open': showSubMenu === 'news'}">
            <a href="#" title="最新消息" @click="toggleSubMenu('news')">最新消息</a>
            <ul>
              <li><a href="#" title="最新公告">最新公告</a></li>
              <li><a href="#" title="活動資訊">活動資訊</a></li>
            </ul>
          </li>
          <li class="has-child" :class="{'is-open': showSubMenu  === 'works'}">
            <a href="#" title="作品集" @click="toggleSubMenu('works')">作品集</a>
            <ul>
              <li><a href="#" title="智慧生活">智慧生活</a></li>
              <li><a href="#" title="友善校園">友善校園</a></li>
            </ul>
          </li>
        </ul>
      </nav>

      <!-- nav links -->
      <ul class="nav-links">
        <li class="lang-switch"
          :class="{'is-open': langOpen}">
          <a href="#" @click.prevent="langOpen = !langOpen">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"  fill="none" stroke="currentColor" stroke-width="1" stroke-linecap="round"  stroke-linejoin="round" class="icon icon-tabler icons-tabler-outline icon-tabler-world"><path stroke="none" d="M0 0h24v24H0z" fill="none"/><path d="M3 12a9 9 0 1 0 18 0a9 9 0 0 0 -18 0" /><path d="M3.6 9h16.8" /><path d="M3.6 15h16.8" /><path d="M11.5 3a17 17 0 0 0 0 18" /><path d="M12.5 3a17 17 0 0 1 0 18" /></svg>
          </a>
          <ul class="reset">
            <!-- 當前語系 .current -->
            <li><a href="javascript:void(0);" class="current" title="繁中">繁中</a></li>
            <li><a href="javascript:void(0);" title="EN">EN</a></li>
          </ul>
        </li>
        <li><!-- Search -->
          <a href="#" class="search-switch"
          :class="{'is-open': searchOpen}" @click.prevent="searchOpen = !searchOpen">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round" class="icon icon-tabler icons-tabler-outline icon-tabler-search" aria-hidden="true"><path stroke="none" d="M0 0h24v24H0z" fill="none"/><path d="M10 10m-7 0a7 7 0 1 0 14 0a7 7 0 1 0 -14 0" /><path d="M21 21l-6 -6" /></svg>
          </a>
        </li>
      </ul>

      <!-- Navigation Switch -->
      <a href="#" class="nav-switch" title="點擊前往主導覽"
      :class="{'is-open': isOpen}" @click.prevent="toggleNav">
        <span></span>
        <span></span>
        <span></span>
      </a>
    </div>

    <!-- search popup -->
    <div class="search-popup" :class="{'is-open': searchOpen}">
      <form action="SearchResult.html" name="form_search" class="search-group">
        <label for="search_keyword" class="search-label">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24"  viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round" class="icon icon-tabler icons-tabler-outline icon-tabler-search" aria-hidden="true"><path stroke="none" d="M0 0h24v24H0z" fill="none"/><path d="M10 10m-7 0a7 7 0 1 0 14 0a7 7 0 1 0 -14 0" /><path d="M21 21l-6 -6" /></svg>
          <input type="search" name="search_keyword" class="search-input"
          autocomplete="off" placeholder="搜尋關鍵字..." />
        </label>

        <button type="submit" class="search-send" title="開始搜尋">
          Search
        </button>
      </form>
      <a class="search-close" href="#" title="關閉搜尋"
      @click.prevent="searchOpen = !searchOpen">
        <span class="sr-only">關閉搜尋</span>
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#1FAC79" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round" class="icon icon-tabler icons-tabler-outline icon-tabler-x"><path stroke="none" d="M0 0h24v24H0z" fill="none"/><path d="M18 6l-12 12" /><path d="M6 6l12 12" /></svg>
      </a>
    </div>
  </header>
</template>

<script setup>
import { onMounted, onUnmounted, ref } from 'vue';
import MobileDetect from 'mobile-detect';

const isOpen = ref(false);
const searchOpen = ref(false);
const langOpen = ref(false);

const toggleNav = () => {
  isOpen.value = !isOpen.value;

  if (isOpen.value) {
    searchOpen.value = false;
    langOpen.value = false;
  }
};

// 改變視窗返回預設值
const handleResize = () => {
  isOpen.value = false;
  searchOpen.value = false;
  langOpen.value = false;
};

// 次選單點擊
const showSubMenu = ref(null);
const toggleSubMenu = (menu) => {
  if (showSubMenu.value === menu) {
    showSubMenu.value = null;
  } else {
    showSubMenu.value = menu;
  }
};

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

  // 改變視窗大小時,呼叫 handleResize
  window.addEventListener('resize', handleResize);
});
// 元件卸載時移除監聽事件
onUnmounted(() => {
  window.removeEventListener('resize', handleResize);
});

</script>
<style lang="scss" scoped>

</style>
