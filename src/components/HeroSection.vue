<script setup lang="ts">
import BmiCalculator from '@/components/BmiCalculator.vue'
import logo from '@/assets/images/logo.svg'
</script>

<template>
  <section class="hero-section">
    <div class="container hero-container">
      <div class="hero">
        <div class="hero__content">
          <img class="hero__logo" :src="logo" alt="logo" />
          <h1 class="hero__heading heading-primary">Body Mass Index Calculator</h1>
          <p class="hero__description">
            Better understand your weight in relation to your height using our body mass index (BMI)
            calculator. While BMI is not the sole determinant of a healthy weight, it offers a
            valuable starting point to evaluate your overall health and well-being.
          </p>
        </div>
      </div>
      <div class="bmi-calculator-container">
        <BmiCalculator>
          <template #heading>
            <h2 class="heading-tertiary">Enter your details below</h2>
          </template>
        </BmiCalculator>
      </div>
    </div>
  </section>
</template>
<style scoped lang="scss">
.hero-section {
  @include pseudo() {
    inset: 0;
    height: 64rem;
    background: linear-gradient(290deg, #d6e6fe 0%, rgba(214, 252, 254, 0) 100%);
    border-radius: 0 0 50px 50px;
  }
  .hero-container {
    position: relative;
  }
  .bmi-calculator-container {
    position: relative;
    margin-top: -22rem;
  }

  .hero {
    position: relative;
    padding-top: 3.2rem;
    text-align: center;
    height: 64rem;

    &__logo {
      width: 4rem;
      height: 4rem;
    }

    &__content {
      display: flex;
      flex-direction: column;
      gap: 2.4rem;
      align-items: center;
      text-align: center;
      margin-right: var(--horizontal-spacing);
    }

    &__heading {
      text-wrap: balance;
    }

    &__description {
      max-width: 46.5rem;
    }
  }
}

@include media-breakpoint-up(lg) {
  .hero-section {
    max-width: 140rem;
    height: 73.7rem;
    margin-inline: auto;

    @include pseudo() {
      width: 97.8rem;
      height: 100%;
    }
    .bmi-calculator-container {
      max-width: 56.4rem;
      position: absolute;
      width: 37vw;
      right: 0;
      top: 16.7rem;
      margin-top: unset;
    }

    .hero {
      &__logo {
        width: 6.4rem;
        height: 6.4rem;
        margin-bottom: 12.7rem;
      }

      &__content {
        max-width: 56.4rem;
        align-items: start;
        text-align: left;
        margin-right: unset;
        gap: 3.5rem;
      }
    }
  }
}
</style>
