<script setup lang="ts">
import gender from '@/assets/images/icon-gender.svg'
import age from '@/assets/images/icon-age.svg'
import muscle from '@/assets/images/icon-muscle.svg'
import pregnancy from '@/assets/images/icon-pregnancy.svg'
import race from '@/assets/images/icon-race.svg'

import BaseCard from '@/components/ui/BaseCard.vue'

interface Limitation {
  icon: string
  heading: string
  description: string
}

const limitations: Limitation[] = [
  {
    icon: gender,
    heading: 'Gender',
    description:
      "The development and body fat composition of girls and boys vary with age. Consequently, a child's age and gender are considered when evaluating their BMI."
  },
  {
    icon: age,
    heading: 'Age',
    description:
      'In aging individuals, increased body fat and muscle loss may cause BMI to underestimate body fat content.'
  },
  {
    icon: muscle,
    heading: 'Muscle',
    description:
      "BMI may misclassify muscular individuals as overweight or obese, as it doesn't differentiate muscle from fat."
  },
  {
    icon: pregnancy,
    heading: 'Pregnancy',
    description:
      'Expectant mothers experience weight gain due to their growing baby. Maintaining a healthy pre-pregnancy BMI is advisable to minimise health risks for both mother and child.'
  },
  {
    icon: race,
    heading: 'Race',
    description:
      'Certain health concerns may affect individuals of some Black and Asian origins at lower BMIs than others. To learn more, it is advised to discuss this with your GP or practice nurse.'
  }
]
</script>

<template>
  <section class="limitations-section">
    <div class="container">
      <div class="limitations">
        <div class="limitation-desc-container">
          <h2 class="heading-secondary">Limitations of BMI</h2>
          <p>
            Although BMI is often a practical indicator of healthy weight, it is not suited for
            every person. Specific groups should carefully consider their BMI outcomes, and in
            certain cases, the measurement may not be beneficial to use.
          </p>
        </div>
        <BaseCard
          class="limitation"
          v-for="({ icon, heading, description }, index) in limitations"
          :key="index"
        >
          <div class="header">
            <img alt="" width="32" height="32" :src="icon" />
            <h3 class="heading-quaternary">{{ heading }}</h3>
          </div>
          <p>{{ description }}</p>
        </BaseCard>
      </div>
    </div>
  </section>
</template>

<style scoped lang="scss">
.limitations-section {
  margin-block: 7.2rem;
}

.limitations {
  grid-template-columns: 1fr;
  display: grid;
  gap: 1.6rem;
}

.limitation-desc-container {
  text-align: center;
  .heading-secondary {
    margin-bottom: 3.2rem;
  }

  p {
    margin-bottom: 3.2rem;
  }
}

.limitation {
  .header {
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 1.6rem;
    margin-bottom: 1.6rem;
  }
}

@include media-breakpoint-up(md) {
  .limitations-section {
    margin-block: 9.6rem;
  }

  .limitations {
    grid-template-columns: repeat(4, 1fr);
    row-gap: 2.4rem;
    column-gap: 1.5rem;

    .limitation-desc-container {
      text-align: center;
      grid-column: 1 / -1;
    }

    .limitation {
      grid-column: span 2;
    }

    .limitation:nth-child(6) {
      grid-column: 2 / 4;
    }
  }
}

@include media-breakpoint-up(xl) {
  .limitations-section {
    margin-block: 12rem;
  }
  .limitations {
    grid-template-columns: repeat(3, 1fr);
    row-gap: 2.4rem;
    column-gap: 1.5rem;
    background-image: url(@/assets/images/pattern-curved-line-right.svg);
    background-repeat: no-repeat;
    background-position: top calc(50% - 4.5rem) left 16rem;

    .limitation-desc-container {
      text-align: left;
      grid-column: 1 / 3;
      max-width: 56.4rem;
    }

    .limitation {
      grid-column: span 1;
    }

    .limitation:nth-child(2) {
      transform: translateX(-10rem);
    }

    .limitation:nth-child(3) {
      grid-column: 2 / 3;
    }

    .limitation:nth-child(5) {
      grid-column: 2 / 3;
      transform: translateX(-20rem);
    }

    .limitation:nth-child(6) {
      grid-column: unset;
      transform: translateX(-20rem);
    }
  }
}
</style>
