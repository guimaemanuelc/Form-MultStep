<template>
  <div class="[ btns ]">
    <button class="[ back ]" v-if="current > 1" @click="handleBackStep">Go Back</button>
    <button class="[ next ]" @click="handleNextStep">Next</button>
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
            if (this.current === this.steps.length - 1) {
                const nextComponent = this.getNextComponent();
                this.$emit('next', nextComponent);
            } else {
                this.$emit('next');
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