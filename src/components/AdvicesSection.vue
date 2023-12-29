<script setup lang="ts">
import eating from '@/assets/images/icon-eating.svg'
import exercise from '@/assets/images/icon-exercise.svg'
import sleep from '@/assets/images/icon-sleep.svg'

interface Advice {
  icon: string
  heading: string
  description: string
}

const advices: Advice[] = [
  {
    icon: eating,
    heading: 'Healthy eating',
    description:
      'Healthy eating promotes weight control, disease prevention, better digestion, immunity, mental clarity, and mood.'
  },
  {
    icon: exercise,
    heading: 'Regular exercise',
    description:
      'Exercise improves fitness, aids weight control, elevates mood, and reduces disease risk, fostering wellness and longevity.'
  },
  {
    icon: sleep,
    heading: 'Adequate sleep',
    description:
      'Sleep enhances mental clarity, emotional stability, and physical wellness, promoting overall restoration and rejuvenation.'
  }
]
</script>
<template>
  <section class="advices-section">
    <div class="container">
      <ul class="even-columns advices">
        <li class="advice" v-for="({ icon, heading, description }, index) in advices" :key="index">
          <img class="advice__icon" alt="" width="64" height="64" :src="icon" />
          <div class="advice__content">
            <h2 class="advice__heading heading-tertiary">{{ heading }}</h2>
            <p class="advice__description">{{ description }}</p>
          </div>
        </li>
      </ul>
    </div>
  </section>
</template>
<style scoped lang="scss">
.advices-section {
  margin-top: 7.2rem;
  margin-inline: auto;
  max-width: 140rem;
  padding-block: 5.6rem;
  border-radius: 3.5rem;
  background: linear-gradient(290deg, rgba(214, 230, 254, 0.25) 0%, rgba(214, 252, 254, 0) 100%);
}

.advices {
  row-gap: 4rem;
  column-gap: 3rem;
}

.advice {
  display: flex;
  flex-direction: column;
  align-items: start;
  gap: 4rem;

  &__icon {
    width: 6.4rem;
    height: 6.4rem;
  }
  &__heading {
    margin-bottom: 2.4rem;
  }
}
@include media-breakpoint-up(md) {
  .advices {
    grid-auto-flow: row;
  }

  .advice {
    gap: 4.5rem;
    flex-direction: row;
    align-items: center;
  }
}
@include media-breakpoint-up(lg) {
  .advice {
    gap: 4.5rem;
    flex-direction: column;
    align-items: start;
  }

  .advices {
    grid-auto-flow: column;
  }
}
</style>
