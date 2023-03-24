<template>
  <div class="[ sidebar ]">
    <div>
        <img src="src/img/bg-sidebar-desktop.svg" alt="" class="sidebar-image">  
    </div>
    
    <div class="[ step-absolute ]">
        <div class="[ step ]" v-for="(step, index) in steps" :key="index">
            <div class="[ index ]">{{ index + 1 }}</div>
            <div>
                <span class="[ current-step ]"> STEP {{ index + 1 }}</span>
                <div class="[ name-step ]">{{ mappedStepName(step) }}</div>
            </div>
      </div>
    </div>
      
  </div>
</template>

<script>
export default {
    name: 'StepSetup',
    props: {
        steps: {
            type: Array,
            default: () => []
        },
        currentStep: {
            type: Number,
            default: 0
        }
    },
    computed: {
      mappedStepNames() {
        return {
          PersonalInfo: 'YOUR INFO',
          SelectPlan: 'SELECT PLAN',
          AddOns: 'ADD-ONS',
          SummaryConfirm: 'SUMMARY'
        }
      }
    },
    methods: {
      mappedStepName(step) {
        return this.mappedStepNames[step] || step;
      }
    }
}
</script>

<style lang="scss" scoped>

    .sidebar {
        position: relative;
        width: 100%;
    }

    img {
        height: 540px;
        margin: 12px;
        position: relative;
    }

    .step {
        color: var(--white);
        display: flex;  
        margin-bottom: 25px;
    }

    .step-absolute {
        position: absolute;
        top: 50px;
        left: 50px;

        .index{
            border: 1px solid var(--white);
            width: 30px;
            height: 30px;
            display: flex;
            margin-right: 12px;
            justify-content: center;
            align-items: center;
            border-radius: 100%;
        }

        .current-step {
            font-size: 12px;
            color: var(--cool-gray);
            padding-bottom: 5px;
        }

        .name-step {
            font-weight: bold;
            margin-top: 1.3px;
        }
    }
</style>