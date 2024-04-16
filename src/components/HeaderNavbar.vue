<template>
  <header class="header">
    <div class="l-container-lg">
      <a href="#" class="logo">
        <img src="../assets/images/logo.svg" />
        <span>Your Company</span>
      </a>

      <!-- Navigation -->
      <nav id="navigation" class="nav">
        <ul class="menu">
          <li>
            <a href="#" title="關於本區">關於本區</a>
          </li>
          <li>
            <a href="#" title="最新消息">最新消息</a>
            <ul>
              <li><a href="#" title="最新消息">最新消息</a></li>
              <li><a href="#" title="活動資訊">活動資訊</a></li>
            </ul>
          </li>
        </ul>
      </nav>

      <!-- Navigation Switch -->
      <a href="#navigation" class="nav-switch" title="點擊前往主導覽">
        <div aria-hidden="true"></div>
        <div aria-hidden="true"></div>
        <div aria-hidden="true"></div>
      </a>
    </div>
  </header>
</template>
<script>
export default {
  setup() {
    return {

    };
  },
};
</script>
<style lang="scss" scoped>

</style>
