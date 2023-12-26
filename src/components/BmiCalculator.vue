<script setup lang="ts">
import { computed, reactive, ref, watch } from 'vue'
import BaseMeasurementInput from './ui/BaseMeasurementInput.vue'
import BaseRadioButton from './ui/BaseRadioButton.vue'

enum MeasurementSystem {
  Metric = 'metric',
  Imperial = 'imperial'
}

interface Props {
  defaultMeasurementSystem?: MeasurementSystem
}

const props = withDefaults(defineProps<Props>(), {
  defaultMeasurementSystem: MeasurementSystem.Metric
})

const MIN_HEALTHY_BMI = 18.5
const MAX_HEALTHY_BMI = 25

const selectedMeasurementSystem = ref(props.defaultMeasurementSystem)
const metric = reactive({ cm: undefined, kg: undefined })
const imperial = reactive({ ft: undefined, in: undefined, st: undefined, lbs: undefined })

const result = computed(() => {
  let weight = 0
  let height = 0
  let bmi = 0

  if (selectedMeasurementSystem.value === MeasurementSystem.Metric) {
    if (metric.cm == undefined || metric.kg == undefined) return undefined

    weight = metric.kg
    height = metric.cm * 0.01
    bmi = weight / height ** 2
  } else {
    if (
      imperial.ft == undefined ||
      imperial.in == undefined ||
      imperial.st == undefined ||
      imperial.lbs == undefined
    )
      return undefined

    weight = imperial.st * 14 + imperial.lbs
    height = imperial.ft * 12 + imperial.in
    bmi = (weight / height ** 2) * 703
  }

  const bmiCategory = getBmiCategory(bmi)
  const healthyWeightRange = getHealthyWeightRange(height, selectedMeasurementSystem.value)

  return {
    bmi: bmi.toFixed(1),
    bmiCategory,
    healthyWeightRange
  }
})

watch(selectedMeasurementSystem, () => {
  setInitialValues()
})

function getBmiCategory(bmi: number) {
  if (bmi < 16) return 'Severely Underweight'
  if (bmi < 18.5 && bmi > 16) return 'Underweight'
  if (bmi < 25 && bmi > 18.5) return 'Healty Weight'
  if (bmi < 30 && bmi > 25) return 'Overweight'
  if (bmi < 35 && bmi > 30) return 'Moderately Obese'
  if (bmi < 40 && bmi > 35) return 'Severely Obese'
  return 'Very Severely Obese'
}

function getHealthyWeightRange(height: number, measurementSystem: MeasurementSystem) {
  let minWeight = 0
  let maxWeight = 0

  if (measurementSystem == MeasurementSystem.Metric) {
    minWeight = MIN_HEALTHY_BMI * height ** 2
    maxWeight = MAX_HEALTHY_BMI * height ** 2

    return {
      minWeight: `${minWeight.toFixed(1)}kgs`,
      maxWeight: `${maxWeight.toFixed(1)}kgs`
    }
  } else {
    minWeight = (MIN_HEALTHY_BMI * height ** 2) / 703
    maxWeight = (MAX_HEALTHY_BMI * height ** 2) / 703

    return {
      minWeight: `${(minWeight / 14).toFixed(0)}st ${(minWeight % 14).toFixed(0)}lbs`,
      maxWeight: `${(maxWeight / 14).toFixed(0)}st ${(maxWeight % 14).toFixed(0)}lbs`
    }
  }
}

function setInitialValues() {
  metric.cm = undefined
  metric.kg = undefined
  imperial.ft = undefined
  imperial.in = undefined
  imperial.st = undefined
  imperial.lbs = undefined
}
</script>

<template>
  <div class="bmi-calculator">
    <slot name="heading">Enter your details below</slot>
    <div class="form-group">
      <div class="radio-input-group">
        <BaseRadioButton
          :name="'measurementSystem'"
          :input-id="'metric'"
          :value="'metric'"
          v-model="selectedMeasurementSystem"
        />
        <label for="metric">Metric</label>
      </div>
      <div class="radio-input-group">
        <BaseRadioButton
          :name="'measurementSystem'"
          :input-id="'imperial'"
          :value="'imperial'"
          v-model="selectedMeasurementSystem"
        />
        <label for="imperial">Imperial</label>
      </div>
    </div>

    <div class="metric" v-if="selectedMeasurementSystem == 'metric'">
      <div class="form-group">
        <div class="input-group">
          <label>Height</label>
          <BaseMeasurementInput
            :name="'height-cm'"
            :input-id="'height-cm'"
            :unit="'cm'"
            :aria-label="'Height in centimeters'"
            v-model="metric.cm"
          />
        </div>
        <div class="input-group">
          <label>Weight</label>
          <BaseMeasurementInput
            :name="'weight-kg'"
            :input-id="'weight-kg'"
            :unit="'kg'"
            :aria-label="'Weight in kilograms'"
            v-model="metric.kg"
          />
        </div>
      </div>
    </div>

    <div class="imperial" v-if="selectedMeasurementSystem == 'imperial'">
      <div class="form-group">
        <label>Height</label>
        <div class="input-group">
          <BaseMeasurementInput
            :name="'height-ft'"
            :input-id="'height-ft'"
            :unit="'ft'"
            :aria-label="'Ft'"
            v-model="imperial.ft"
          />
        </div>
        <div class="input-group">
          <BaseMeasurementInput
            :name="'height-in'"
            :input-id="'height-in'"
            :unit="'in'"
            :aria-label="'in'"
            v-model="imperial.in"
          />
        </div>
      </div>
      <div class="form-group">
        <label>Weight</label>
        <div class="input-group">
          <BaseMeasurementInput
            :name="'weight-st'"
            :input-id="'weight-st'"
            :unit="'st'"
            :aria-label="'st'"
            v-model="imperial.st"
          />
        </div>
        <div class="input-group">
          <BaseMeasurementInput
            :name="'weight-lbs'"
            :input-id="'weight-lbs'"
            :unit="'lbs'"
            :aria-label="'lbs'"
            v-model="imperial.lbs"
          />
        </div>
      </div>
    </div>

    <div class="result-container">
      <div class="welcome" v-if="result == undefined">
        <h2>Welcome!</h2>
        <p>Enter your height and weight and you’ll see your BMI result here</p>
      </div>
      <div v-else class="result">
        <div class="result__bmi">
          <p>Your BMI is...</p>
          <strong>{{ result.bmi }}</strong>
        </div>
        <div class="result__description">
          <p>
            Your BMI suggests you're a {{ result.bmiCategory }}. Your ideal weight is between
            <strong>
              {{ result.healthyWeightRange.minWeight }} -
              {{ result.healthyWeightRange.maxWeight }} </strong
            >.
          </p>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped lang="scss">
.bmi-calculator {
  display: flex;
  padding: 2.4rem;
  flex-direction: column;
  align-items: flex-start;
  gap: 2.4rem;
  border-radius: 1.6rem;
  background-color: #fff;
  box-shadow: 16px 32px 56px 0px rgba(143, 174, 207, 0.25);

  .imperial {
    display: grid;
    gap: 3.2rem;
  }

  .form-group {
    width: 100%;
    display: grid;
    grid-template-columns: 1fr 1fr;
    column-gap: 2.4rem;
    row-gap: 0.8rem;

    label {
      grid-column: span 2 / span 2;
      color: #5e6e85;
      font-size: 1.4rem;
    }
  }

  .radio-input-group {
    display: flex;
    align-items: center;
    gap: 1.8rem;

    label {
      font-weight: var(--fw-semi-bold);
      color: hsl(var(--clr-gunmetal));
    }
  }
  .input-group {
    display: grid;
    gap: 0.8rem;

    label {
      color: #5e6e85;
      font-size: 1.4rem;
    }
  }

  .result-container {
    color: #fff;
    width: 100%;
    border-radius: 1.6rem;
    background: linear-gradient(90deg, #345ff6 0%, #587dff 100%);
    padding: 3.2rem;

    .welcome {
      display: flex;
      flex-direction: column;
      gap: 1.6rem;

      p {
        font-size: 1.4rem;
      }
    }

    .result {
      display: grid;
      gap: 2.4rem;

      &__bmi {
        font-weight: var(--fw-semi-bold);

        p {
          margin-top: 0.8rem;
        }

        strong {
          font-size: 6.4rem;
          font-weight: 600;
          line-height: 110%;
          letter-spacing: -0.32rem;
        }
      }
    }
  }

  @include media-breakpoint-up(lg) {
    gap: 3.2rem;
    padding: 3.2rem;
    .result-container {
      border-top-right-radius: 100px;
      border-bottom-right-radius: 100px;

      .result {
        grid-template-columns: 1fr 1fr;
      }
    }
  }
}
</style>
