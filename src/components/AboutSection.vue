<script setup lang="ts">
import manEating from '@/assets/images/image-man-eating.webp'
</script>
<template>
  <section class="about-bmi-section">
    <div class="container about-bmi-container">
      <div class="even-columns about-bmi">
        <img class="about-bmi__img" alt="" width="1066" height="1128" :src="manEating" />
        <div class="about-bmi__content">
          <h2 class="heading-secondary about-bmi__heading">What your BMI result means</h2>
          <p class="about-bmi__description">
            A BMI range of 18.5 to 24.9 is considered a 'healthy weight.' Maintaining a healthy
            weight may lower your chances of experiencing health issues later on, such as obesity
            and type 2 diabetes. Aim for a nutritious diet with reduced fat and sugar content,
            incorporating ample fruits and vegetables. Additionally, strive for regular physical
            activity, ideally about 30 minutes daily for five days a week.
          </p>
        </div>
      </div>
    </div>
  </section>
</template>
<style scoped lang="scss">
.about-bmi-section {
  margin-top: 7.2rem;
}

.about-bmi {
  &__content {
    padding-top: 4.8rem;
  }

  &__img {
    margin-left: calc(var(--horizontal-spacing) * -1);
    max-width: calc(100% + var(--horizontal-spacing) * 2);
  }

  &__heading {
    margin-bottom: 3.2rem;
  }
}

@include media-breakpoint-up(sm) {
  .about-bmi {
    &__img {
      max-width: 100%;
      margin-left: auto;
      margin-right: auto;
    }
  }
}

@include media-breakpoint-up(md) {
  .about-bmi-section {
    margin-top: 9.6rem;
  }
  .about-bmi-container {
    --horizontal-spacing: 2rem;
    margin-left: 0;
  }
  .about-bmi {
    gap: 7.5rem;
    align-items: center;

    &__content {
      padding-top: unset;
    }
  }
}

@include media-breakpoint-up(xl) {
  .about-bmi-section {
    margin-top: 6.5rem;
  }
  .about-bmi-container {
    --horizontal-spacing: 4rem;
    margin-left: auto;
  }
  .about-bmi {
    gap: 13rem;
    padding-top: unset;

    &__img {
      margin-left: unset;
    }

    &__content {
      position: relative;
      padding-top: 18.4rem;

      @include pseudo($content: url('@/assets/images/pattern-curved-line-left.svg')) {
        top: -5rem;
        right: 2rem;
        width: 8.5rem;
        height: 20rem;
      }
    }
  }
}
</style>
