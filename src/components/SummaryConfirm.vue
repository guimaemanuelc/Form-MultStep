<template>
  <div>
    <div v-if="!showThanks" class="[ finish ]">
      <div class="[ top ]">
        <h1>Finishing up</h1>
        <span>Double-check everything looks OK before confirming.</span>
      </div>

      <div class="[ summary ]">
        <div>
          <div class="[ plan-confirm ]">
            <div class="[ chosen-plan ]">
              <span>Arcade(Monthly)</span>
              <span class="[ value ]">$9/mo</span>
            </div>
            <a href="#" @click="$emit('goToStep', 1)" class="[ change ]">Change</a>
          </div>

          <div class="[ chosen-services ]">
            <div class="[ service ]">
              <span>Online service</span>
              <span class="[ value ]">+$1/mo</span>
            </div>
          </div>
        </div>
      </div>
      <div class="[ sum ]">
        <span>Total (per month)</span>
        <span class="[ total ]">+{{ totalPerMonth }}/mo</span>
      </div>
   </div>
    
      <div v-if="showThanks" class="[ thanks ]">
        <img src="/src/img/icon-thank-you.svg" alt="">
        <h1>Thank you!</h1>
        <p>Thanks for confirming your subscription! We hope you have fun using our platform. If you ever need support, please feel free to email us at support@loremgaming.com.</p>
      </div>

  </div>
</template>

<script>
export default {
  name: 'SummaryConfirm',
  props: ['showThanks']

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

.summary {
  border-radius: var(--border);
  background-color: var(--magnolia);
  padding: 25px;

  span {
    color: var(--cool-gray);
  }

  .plan-confirm {
    border-bottom: 1px solid var(--light-gray);
    display: flex;
    flex-direction: column;
    padding-bottom: 20px;

    .chosen-plan {
      display: flex;
      justify-content: space-between;

      span {
        color: var(--marine-blue);
        font-weight: bold;
      }
    }
    .change {
      color: var(--cool-gray);
      font-size: 14px;
      margin-top: 7px;
      padding: 3px 0;
    }
  }

  .chosen-services {
    margin-top: 13px;

    .service {
      display: flex;
      justify-content: space-between;
    }

    .value {
      color: var(--marine-blue);
    }
  }
}
.sum {
  display: flex;
  justify-content: space-between;
  padding: 25px;
  color: var(--cool-gray);

  .total {
    color: var(--purplish-blue);
    font-weight: bold;
  }
}

.thanks {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 20px;
  margin-top: 120px;

  img {
    width: 60px;
  }

  h1 {
    color: var(--marine-blue);
    font-weight: bold;
    font-size: 1.7rem;
  }

  p {
    color: var(--cool-gray);
    text-align: center;
    font-size: 0.9rem;
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

  .thanks {
    margin-top: 50px;

    p {
      font-size: 1.19rem;
      padding-bottom: 120px;
    }
  }
}
</style>
