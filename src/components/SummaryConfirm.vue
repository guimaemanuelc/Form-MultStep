<template>
  <div>
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
          <a href="#" class="[ change ]">Change</a>  
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
      <span class="[ total ]">+$12/mo</span>
    </div>
  </div>
</template>

<script>
export default {
    name: 'SummaryConfirm'
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

</style>