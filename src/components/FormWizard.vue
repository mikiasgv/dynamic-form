<template>
  <div>
    <component 
      :is="steps[currentStepNumber - 1]"
      @update="processStep"
      :wizard-data="form"
      ></component>

    <div class="progress-bar">
      <div :style="`width: ${progress}%;`"></div>
    </div>

    <!-- Actions -->
    <div class="buttons">
      <button
        @click="goBack"
        v-if="currentStepNumber > 1"
        class="btn-outlined"
      >Back
      </button>
      <button
        @click="goNext"
        class="btn"
      >Next</button>
    </div>

    <pre><code>{{form}}</code></pre>
  </div>
</template>

<script>
import FormPlanPicker from './FormPlanPicker'
import FormUserDetails from './FormUserDetails'
import FormAddress from './FormAddress'
import FormReviewOrder from './FormReviewOrder'
export default {
  name: 'FormWizard',
  components: {
    FormPlanPicker,
    FormUserDetails,
    FormAddress,
    FormReviewOrder
  },
  computed: {
    length() {
      return this.steps.length;
    }
  },
  data () {
    return {
      currentStepNumber: 1,
      form: {
        plan: null,
        email: null,
        name: null,
        password: null,
        address: null,
        recipient: null,
        chocolate: false,
        otherTreat: false
      },
      steps: [
        'FormPlanPicker',
        'FormUserDetails',
        'FormAddress',
        'FormReviewOrder'
      ]
    }
  },
  computed: {
    progress () {
      return this.currentStepNumber/this.length * 100;
    }
  },
  methods: {
    processStep(stepData) {
      Object.assign(this.form, stepData);
    },
    goBack () {
      this.currentStepNumber--;
    },
    goNext () {
      this.currentStepNumber++;
    }
  }
}
</script>
