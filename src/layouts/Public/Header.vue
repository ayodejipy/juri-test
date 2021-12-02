<template>
  <div class="header">
    <div class="logo-container" :class="[{'page2-left-padding': currentPage == 'page-2' || currentPage == 'page-3' }]">
      <img
        class="logo"
        alt="Juridoc Logo"
        v-lazy="{ src: '/images/logo.png' }"
      />
    </div>
    <div class="selector" :class="[
      {'page2-right-padding': currentPage == 'page-2'},
      {'page3-right-padding': currentPage == 'page-3'}
    ]">
      <span>{{step}}</span>
      <SelectLang v-model="currentLang" />
    </div>
  </div>
</template>

<script lang="ts">
import {
  computed, defineComponent, ref, watch,
} from 'vue';
import { useI18n } from 'vue-i18n';
import { useRoute } from 'vue-router';
import SelectLang from '@/layouts/Public/SelectLang.vue';

export default defineComponent({
  components: { SelectLang },
  setup() {
    const langStorage = localStorage.getItem('lang');
    const currentLang = ref(langStorage || 'br');
    const i18n = useI18n();
    const route = useRoute();

    watch(currentLang, (newValue) => {
      window.localStorage.setItem('lang', newValue);
      i18n.locale.value = newValue;
    });

    const step = computed(() => {
      if (route.name === 'RegisterStep2') return i18n.t('Step2.form.prelude');
      if (route.name === 'RegisterStep3') return i18n.t('Step3.form.prelude');
      return '';
    });
    
    const currentPage = computed(() => {
      if (route.name === 'RegisterStep2') return 'page-2';
      if (route.name === 'RegisterStep3') return 'page-3';
      return ''
    })
    return { currentLang, currentPage, step, t: i18n.t };
  },
});
</script>

<style lang="scss" scoped>
.header {
  border-radius: 5px 5px 0px 0px;
  display: grid;
  grid-column: 1/3;
  grid-template-columns: 510px 480px;
  height: 80px;

  .logo-container {
    border-radius: 5px 0px 0px 0px;
    padding-top: 50px;
    background-color: $neutral-bg ;
    padding-left: 60px;
    /* padding: 30px 60px 50px 60px; */
    img {
      width: 110px;
      height: auto;
    }
  }
  .selector {
    border-radius: 0px 5px 0px 0px;
    /* padding-top: 30px;
    padding-right: 60px;
    padding-left: 70px; */
    padding: 50px 60px 0 60px;
    width: 100%;
    background-color: $white;
    justify-content: space-between;
    display: flex;
    span {
      color: $text-dark-grey-6;
      font-size: 14px;
      line-height: 27px;
    }
    
    @media only screen and (max-width: 768px) {
      padding: 10px 12px;
      flex-direction: row;
    }
  }
  .page2-left-padding {
    padding: 50px 70px 0 70px;
    
    @media only screen and (max-width: 768px) {
      flex-direction: row;
      padding: 13px 3px;
    }
  }
  .page2-right-padding {
    padding: 50px 60px 0 60px;
    
    @media only screen and (max-width: 768px) {
      justify-content: space-between;
      padding-right: 0;
    }
  }
  .page3-right-padding {
    padding: 50px 40px 0 40px;
    @media only screen and (max-width: 768px) {
      padding: 0;
    }
  }
  .page3-right-padding {
    padding: 50px 40px 0 40px;
    @media only screen and (max-width: 768px) {
      padding: 0;
    }
  }
}

@media (orientation: portrait) {
  .header {
    display: flex;
    flex-direction: column;
    height: fit-content;
    justify-content: center;
    
    .logo-container {
      border-radius: 5px 5px 0px 0px;
      padding-top: 27px;
      background-color: $neutral-bg ;
      padding-left: 10%;
      img {
        width: 110px;
        height: auto;
      }
      @media only screen and (max-width: 768px) {
        /* padding-right: 20px;
        padding-left: 20px; */
        padding: 32px 20px 22px;
      }
    }
    .selector {
      border-radius: 0px 0px 0px 0px;
      padding-right: 10%;
      padding-top: 27px;
      width: 100%;
      background-color: $neutral-bg ;
      justify-content: flex-end;
      display: flex;
      
      @media only screen and (max-width: 768px) {
        display: flex;
        justify-content: space-between;
        padding: 18px 20px;
      }
    }

  }
}
</style>
