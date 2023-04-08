<template>
  <div class="[ container ]">
    <div class="[ container-form ]">
      <div class="[ steps ]">
        <step-setup :currentStep="currentStep" :steps="steps" />
      </div>

      <div class="[ infos ]">
        <div class="[ all-forms ]">
          <component
            @inputValue="setUserData"
            @beforeAction="beforeAction = $event"
            @goToStep="currentStep = $event"
            :user="user"
            :is="currentComponent"
            class="[ component ]"
            :showThanks="showThanks"
            @cardSelected="onCardSelected"
            v-on:selectedAddons="handleSelectedAddons"
          />
        </div>

        <div class="[ control ]">
          <step-control
            :steps="steps"
            :current="currentStep"
            @next="handleNextStep"
            @back="currentStep--"
            @toggleShowThanks="alterarShowThanks()"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import StepControl from '../components/StepControl.vue'
import StepSetup from '../components/StepSetup.vue'
import SelectPlan from '../components/SelectPlan.vue'
import SummaryConfirm from '../components/SummaryConfirm.vue'
import AddOns from '../components/AddOns.vue'
import PersonalInfo from '../components/PersonalInfo.vue'

export default {
  name: 'RegistrationPage',
  components: { StepControl, StepSetup, SelectPlan, SummaryConfirm, PersonalInfo, AddOns },
  data() {
    return {
      currentStep: 0,
      steps: ['PersonalInfo', 'SelectPlan', 'AddOns', 'SummaryConfirm'],
      user: {
        name: '',
        email: '',
        phone: '',
        plan: {
          type: 'month'
        }
      },
      beforeAction: null,
      showThanks: false,
    }
  },
  computed: {
    currentComponent() {
      return this.steps[this.currentStep]
    }
  },
  methods: {
    setUserData(args) {
      this.user = {
        ...this.user,
        ...JSON.parse(JSON.stringify(args))
      }
    },
    handleNextStep() {
      let isValid = true
      if (this.beforeAction) {
        isValid = this.beforeAction()
      }

      if (isValid) {
        this.currentStep++
      }
    },
    alterarShowThanks() {
      this.showThanks = !this.showThanks
    },
    onCardSelected(card) {
      this.user.plan = card    
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
  background-color: var(--magnolia);
  font-family: 'Ubuntu';

  &-form {
    -webkit-box-shadow: 1px 0px 14px -8px rgba(0, 0, 0, 0.66);
    -moz-box-shadow: 1px 0px 14px -8px rgba(0, 0, 0, 0.66);
    box-shadow: 1px 0px 14px -8px rgba(0, 0, 0, 0.66);
    width: 56.25rem;
    height: 35.313rem;
    border-radius: var(--border);
    display: flex;
    background-color: var(--white);

    .steps {
      width: 23.75rem;
    }

    .infos {
      margin-top: 50px;
      display: flex;
      flex-direction: column;

      .all-forms {
        height: 26.875rem;
        width: 26.25rem;
      }
    }
  }
}
@media only screen and (max-width: 920px) {
  .container-form {
    width: 44.375rem;

    .steps {
      width: 18.75rem;
    }    

    .infos {
      .all-forms {
      width: 100%;
    }
    }
  }
}

@media only screen and (max-width: 770px) {
  .container {
    align-items: start;  
    height: 90vh;    

    .container-form {
      flex-direction: column;
      width: 21.875rem;
      height: 250px;
      

      .steps {
        width: 100%;
      }

      .infos {
        height: 0px;
      }

      .component {
        width: 19.375rem;
        margin: 10px 15px;
      }

      .all-forms {
        background-color: var(--white);
        position: absolute;
        top: 100px;
        height: auto;
        width: 350px;
        padding-top: 15px;
        padding-left: 5px;
        border-radius: var(--border);
        -webkit-box-shadow: 1px 5px 16px -15px rgba(0,0,0,0.56);
        -moz-box-shadow: 1px 5px 16px -15px rgba(0,0,0,0.56);
        box-shadow: 1px 5px 16px -15px rgba(0,0,0,0.56);
      }
    }

    .control {
      position: absolute;
      bottom: 15px;
      right: 15px;
      width: 92%;
    }
  }
}
</style>

