<template>
  <div class="[ btns ]">
    <button class="[ back ]" v-if="current > 1" @click="handleBackStep">Go Back</button>
    <button class="[ next ]" :class="{ confirm: current === steps.length - 1 }" @click="handleNextStep">{{ current === steps.length - 1 ? 'Confirm' : 'Next' }}</button>
 </div>
</template>

<script>
export default {
    name: 'StepControl',
    props: {
        steps: {
            type: Array,
            default: () => []
        },
        current: {
            type: Number,
            default: 0,
        }
    },
    methods: {
        handleNextStep() {
            const nextComponent = this.getNextComponent();
            if (this.current === this.steps.length - 1) {
                this.$emit('next', this.steps[this.current]);
            } else {
                this.$emit('next', nextComponent);
            }
        },
        handleBackStep() {
            this.$emit('back')
        },
        getNextComponent() {
            if (this.current === this.steps.length - 1) {
                return this.steps[0];
            }
            return this.steps[this.current + 1];
        }
    }
}
</script>

<style lang="scss" scoped>
    .btns {     
        display: flex;
        justify-content: space-between;

        .back {
            border: none;
            background: var(--white);
            color: var(--cool-gray);
            font-weight: bold;
            cursor: pointer;

            &:hover {
                color:var(--marine-blue);
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
        }
    }
</style>