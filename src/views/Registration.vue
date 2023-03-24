<template>
  <div class="[ container ]">
    <div class="[ container-form ]">
      <div class="[ steps ]">
        <step-setup :current="currentStep" :steps="steps"/>
      </div>

      <div class="[ infos ]">

        <div class="[ all-forms ]">
          <component :is="currentComponent"/>
        </div>
       
        <div class="[ control ]">
          <step-control
            :current="currentStep"
            @next="currentStep++"
            @back="currentStep--"
          />  
        </div>  

      </div>
    </div>  
  </div>
</template>

<script>
import StepControl from '../components/StepControl.vue';
import StepSetup from '../components/StepSetup.vue';
import SelectPlan from '../components/SelectPlan.vue';
import SummaryConfirm from '../components/SummaryConfirm.vue';
import AddOns from '../components/AddOns.vue';
import PersonalInfo from '../components/PersonalInfo.vue';

export default {
  name: 'RegistrationPage',
  components: {StepControl, StepSetup, SelectPlan, SummaryConfirm, PersonalInfo, AddOns},
  data() {
    return {
      currentStep: 1,
      steps: [
            'PersonalInfo',
            'SelectPlan',
            'AddOns',
            'SummaryConfirm'
        ]
    }
  },
  computed: {
    currentComponent() {
      return this.steps[this.currentStep - 1];
    }
  },
  methods: {
    handleNextStep() {
      if (this.currentStep < this.steps.length) {
        this.currentStep++;
      }
    },
    handleBackStep() {
      if (this.currentStep > 1) {
        this.currentStep--;
      }
    }
  }
  
}
</script>

<style lang="scss">
  .container {
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color:  var(--magnolia);
    font-family: 'Ubuntu';

    &-form {
      -webkit-box-shadow: 1px 0px 14px -8px rgba(0,0,0,0.66);
      -moz-box-shadow: 1px 0px 14px -8px rgba(0,0,0,0.66);
      box-shadow: 1px 0px 14px -8px rgba(0,0,0,0.66);
      width: 900px;
      height: 565px;
      border-radius: var(--border);
      display: flex;
      background-color: var(--white);


      .steps {
        width: 380px;
      }

      .infos {
        margin-top: 50px;
        display: flex;
        flex-direction: column;

        .all-forms {
          height: 430px;
          width: 420px;
        }
      }
    }
  }

  
</style>
