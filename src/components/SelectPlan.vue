<template>
  <div class="[ container-plan ]">
    <div class="[ top ]">
      <h1>Select your plan</h1>
      <span>You have the option of monthly or yearly biling.</span>
    </div>

    <div class="[ cards ]">
      <div  v-for="(card, index) in cards" :key="index" class="[ card ]"
        v-bind:class="{'selected': index === selectedCardIndex}"
        @click="selectedCardIndex = index">
        <img :src="card.img">
        <div class="[ plan ]">
          <h3>{{ card.plan }}</h3>

          <div v-if="!isYearlyBilling">
            <span>${{ card.price }}/mo</span>
          </div>
          
          <div v-if="isYearlyBilling">
            <span>${{ card.priceYearly }}/yr</span>
            <div class="[ free-month ]">2 months free</div>
          </div>
        </div>  
      </div>
    </div>

    <div class="duration">
      <span :class="{ 'highlighted': !isYearlyBilling }">Monthly</span>
      <label class="[ switch ]">
        <input type="checkbox" @change="onChangeBillingType">
        <span class="[ slider ]"></span>
      </label>
      <span :class="{ 'highlighted': isYearlyBilling }">Yearly</span>
    </div>

  </div>
</template>

<script>

export default {
    name: 'SelectPlan',
    data() {
      return {
        cards: [
          {img: 'src/img/icon-arcade.svg', plan: 'Arcade', price: 9, priceYearly: 90},
          {img: 'src/img/icon-advanced.svg', plan: 'Advanced', price: 12, priceYearly: 120},
          {img: 'src/img/icon-pro.svg', plan: 'Pro', price: 15, priceYearly: 150},
        ],
        isYearlyBilling: false,
        selectedCardIndex: null,
        selectedPlan: null
      }
    },
    computed: {
      selectedCard() {
        return this.cards[this.selectedCardIndex]
      }
    },
    watch: {
      selectedCard() {
        this.$emit('cardSelected', this.selectedCard)
      }
    },
    methods: {
      onChangeBillingType() {
        this.isYearlyBilling = !this.isYearlyBilling
      },
      onSelectedCard(card) {
        this.$emit('cardSelected', card)
      }
    },
}
</script>

<style lang="scss" scoped>
  .top {
    margin-bottom: 35px;

    h1 {
      font-size: 2rem;
      font-weight: bold;
      color: var(--marine-blue);
      margin-bottom: 10px;
    }

    span {
      color: var(--cool-gray);
      font-size: 14px;   
    }
  }

  .cards {
    display: flex;
    gap: 20px;
    
    .card {
      display: flex;
      flex-direction: column;
      justify-content: space-around;
      border: 1px solid var(--light-gray);
      border-radius: var(--border);
      height: 140px;
      width: 130px;
      padding-left: 12px;
      cursor: pointer;

      &.selected {
        border: 2px solid var(--pastel-blue);
      }


        img {
        height: 30px;
        width: 40px;
        }

        .plan {
          h3 {
            color: var(--marine-blue);
            font-weight: bold;
            margin-bottom: 3px;
          }

          span {
            font-size: 14px;
            color: var(--cool-gray);
          }

          .free-month {
            color: var(--marine-blue);
            font-size: 13px;
            margin-top: 5px;
          }
        }
    }   
  }

.duration {
  width: 98%;
  background-color: var(--magnolia);
  display: flex;
  justify-content: center;
  column-gap: 15px;
  color: var(--cool-gray);
  margin-top: 32px;
  height: 40px;
  align-items: center;
  border-radius: var(--border);

  .highlighted {
    color: var(--marine-blue);
    font-weight: bold;
  }

    .switch {
      font-size: 11px;
      position: relative;
      display: inline-block;
      width: 3.7em;
      height: 1.8em;


    .switch input {
      display: none;
      opacity: 0;
      width: 0;
      height: 0;
    }

    .slider {
      position: absolute;
      cursor: pointer;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: var(--marine-blue);
      transition: .2s;
      border-radius: 30px;
    }

    .slider:before {
      position: absolute;
      content: "";
      height: 1.4em;
      width: 1.4em;
      border-radius: 20px;
      left: 0.2em;
      bottom: 0.2em;
      background-color: var(--white);
      transition: .4s;
    }
    input:checked + .slider:before {
      transform: translateX(1.9em);
    }
  }
}
@media only screen and (max-width: 770px) {
  .top{
    h1 {
      margin-bottom: 15px;
    }

    span {
      font-size: 1.2rem;
    }
  }
  .cards {
    flex-direction: column;
    gap: 10px;

    .card {
      flex-direction: row;
      justify-content: start;
      align-items: center;
      width: auto;
      height: 70px;
      gap: 10px;

      .plan {
        h3 {
          margin-bottom: 5px;
        }
      }
    }
  }
  .duration {
    margin-top: 25px;
    margin-bottom: 20px;
    height: 50px;
    width: auto;
  }
}
</style>