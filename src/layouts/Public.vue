<template>
  <div class="login-page">
    <div class="login-card">
      <Header />
      <router-view />
    </div>
  </div>
</template>

<script lang="ts">
import Header from '@/layouts/Public/Header.vue';

export default {
  components: { Header },
};
</script>

<style lang="scss" scoped>
.login-card {
  display: grid;
  grid-template-columns: 510px 480px;
  width: 990px;
  height: fit-content;
  
  @media only screen and (max-width: 768px) {
    width: 100%;
    padding: 0 16px;
  }
}

/* @media screen and (max-width: 1060px) {
  .login-card {
    width: 90%;
    padding: 0px 50px;
  }
} */

@media screen and (max-width: 768px) {
  .login-page {
    width: 100%;
    padding: 45px 16px;
  }
}
/* @media screen and (max-width: 678px) {
  .login-page {
    width: 100%;
    padding: 45px 16px;
  }
} */

@media (orientation: portrait) {
  .login-card {
    display: flex;
    flex-direction: column;
  }
}
</style>
