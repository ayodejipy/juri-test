<template>
  <div class="description">
    <h1>{{ t(`Step2.description.main`) }}</h1>
    <p>{{ t(`Step2.description.sub`) }}</p>
    <div class="lawyer-image-container">
      <img
        class="descriptive"
        v-lazy="{ src: '/images/login/Felipe-Novak-juridoc-socio.png' }"
        alt="Felipe Novak picture"
      />
      <div class="legend">
        <span>Felipe Novak</span>
        <span>{{ t(`Step2.description.lawyerSub`) }}</span>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { useI18n } from 'vue-i18n';

export default defineComponent({
  setup() {
    const { t } = useI18n();

    return { t };
  },
});
</script>

<style lang="scss" scoped>
div.description {
  padding: 30px 70px 50px 70px;
  
  h1 {
    flex-grow: .35;
  }
  img.descriptive {
    width: 100px;
  }
  
  @media screen and (max-width: 768px) {
    padding: 25px 20px;
    
    img.descriptive {
      width: 50px;
    }
  }
}
.lawyer-image-container {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  gap: 1rem;
  
  .legend {
    display: flex;
    flex-direction: column;
    span {
      color: $text-dark-grey;
    }
  }
  
  @media screen and (max-width: 768px) {
    justify-content: flex-start;
  }
}
</style>
