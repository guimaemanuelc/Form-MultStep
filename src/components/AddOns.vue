<template>
  <div>
    <div class="[ top ]">
      <h1>Pick add-ons</h1>
      <span>Add-ons help enhance your gaming experience.</span>
    </div>

    <div class="[ all-services ]">
      <div class=" [ service ]" v-for="(service, index) in services" :key="index" :class="{'selected': service.selected}" @click="toggleSelection(service)">
        <input class="check" type="checkbox" v-model="service.selected">

        <div class="[ division ]">
          <div class="[ type-service ]">
          <h3>{{ service.name }}</h3>
          <span>{{ service.text }}</span>
        </div>   

        <div class="[ price ]">
          <span>+${{ service.price }}/mo</span>
        </div>
        </div>
   
      </div>
    </div>

  </div>
</template>

<script>
export default {
    name: 'AddOns',
    data() {
      return {
        services: [
          {name: 'Online service', text: 'Acces to multiplayer games', price: 1, priceYearly: 10},
          {name: 'Larger storage', text: 'Extra 1TB of cloud save', price: 2},
          {name: 'Customizable Profile', text: 'Custon theme on your profile', price: 2},
        ]
      }
    },
    methods: {
      toggleSelection(service) {
        service.selected = !service.selected;
        this.emitSelectedAddons();
    },
      emitSelectedAddons() {
        const selectedServices = this.services.filter(service => service.selected);
        this.$emit('selectedAddons', selectedServices);
  }
  }
}
</script>

<style lang="scss" scoped>
  .top {
    margin-bottom: 35px;

    h1 {
      font-size: 2rem;
      font-weight: 600;
      color: var(--marine-blue);
      margin-bottom: 10px;
    }

    span {
      color: var(--cool-gray);
      font-size: 14px;   
    }
  }

  .all-services{
    display: flex;
    flex-direction: column;
    gap: 15px;
    padding-bottom: 10px;
    .service {
      display: flex;
      border: 1px solid var(--cool-gray);
      border-radius: var(--border);
      align-items: center;
      height: 70px;
      cursor: pointer;

      .check {
        width: 22px;
        height: 18px;
        margin: 0 12px;
      }

      .division {
        display: flex;
        align-items: center;
        justify-content: space-between;
        width: 82%;
      }
      .type-service {
  
        h3 {
          color: var(--marine-blue);
          font-weight: 600;
          margin-bottom: 4px;
        }
  
        span {
          color: var(--cool-gray);
          font-size: 14px;
        }
      }

      .price {
        color: var(--purplish-blue);
      }

      &.selected {
        background-color: var(--magnolia);
        border: 1px solid var(--marine-blue);
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
}
</style>