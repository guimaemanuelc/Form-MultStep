<template>
  <div class="[ container-personal ]">
    <div class="[ top ]">
        <h1>Personal Info</h1>
        <span>Please provide your name, email address, and phone number.</span>
    </div>

    <div class="[ form-info ]" v-for="(info, index) in infos" :key="index">
      <div class="[ validation ]">
        <label>{{ info.label }}</label>
        <span v-if="!formData[info.key]" class="[ error ]">This field is required</span>
      </div>
      <input type="{{ info.type }}" :placeholder="placeholderText(info)">
    </div>
  </div>
</template>

<script>
export default {
    name: 'PersonalInfo',
    data() {
      return {
        infos: [
          {label: 'Name', type: 'text', placeholder:'e.g. Stehpen King'},
          {label: 'Email Address', type: 'email', placeholder:'e.g. stephenking@lorem.com'},
          {label: 'Phone Number', type: 'number', placeholder:'e.g. +1 234 567 890'}
        ],
        formData: {
          name: '',
          email: '',
          phone: ''
        }
      }
    },
    methods: {
      placeholderText(info) {
        return info.placeholder;
      },
    }
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

  .form-info {
    display: flex;
    flex-direction: column;
    margin-bottom: 22px;

    label {
      color: var(--marine-blue);;
    }

    input {
      margin-top: 10px;
      border-radius: var(--border);
      border: 1px solid var(--light-gray);
      height: 40px;
      font-weight: bold;
      color: var(--marine-blue);
      padding-left: 20px;

      &::placeholder {
        color: var(--cool-gray);
      }

      &:focus {
        outline: 1px solid var(--marine-blue);
      }

    }

    .validation {
      display: flex;
      justify-content: space-between;
    }
    .error {
      color: red;
      margin-left: auto;
      font-size: 14px;
    }
  }

</style>