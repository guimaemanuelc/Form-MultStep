<template>
    <div class="[ btns ]" v-if="!isConfirmed">
      <button class="[ back ]" v-if="current > 0" @click="handleBackStep">Go Back</button>
      <button class="[ next ]" :class="{ confirm: isLastStep }" :style="{ backgroundColor: isLastStep ? 'var(--purplish-blue)' : '' }" @click="handleNextStep">
        {{ isLastStep ? 'Confirm' : 'Next Step' }}
      </button>
    </div>
  </template>
  
<script>
  export default {
    name: 'StepControl',
    data() {
      return {
        isConfirmed: false
      }
    },
    props: {
      steps: {
        type: Array,
        default: () => []
      },
      current: {
        type: Number,
        default: 0
      },
      hidePreviusContent: {
        type: Boolean,
        default: false
      }
    },
    computed: {
      isLastStep() {
      return this.current === this.steps.length - 1
    }
    },
    methods: {
      handleNextStep() {
        if (this.isLastStep) {
          this.isConfirmed = true;
          this.$emit('toggleShowThanks')
        } else if (this.current < this.steps.length - 1) {
          this.$emit('next')
        }
      },
      handleBackStep() {
        this.$emit('back')
      }
    }
  }
</script>
  
  <style lang="scss" scoped>
  .btns {
    display: flex;
    justify-content: space-between;
    background-color: var(--white);
  
    .back {
      border: none;
      background: var(--white);
      color: var(--cool-gray);
      font-weight: bold;
      cursor: pointer;
      padding: 10px;
  
      &:hover {
        color: var(--marine-blue);
      }
    }
  
    .next {
      width: 100px;
      height: 40px;
      border-radius: var(--border);
      background-color: var(--marine-blue);
      color: var(--white);
      cursor: pointer;
      margin-left: auto;

      &.confirm {
        background-color: var(--purplish-blue);
        border: none;
      }
    }
  }

  @media only screen and (max-width: 770px) {
    .btns {
      background-color: var(--white);
      
    }
  }
  </style>
  