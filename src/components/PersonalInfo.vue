<template>
  <div class="[ container-personal ]">
    <div class="[ top ]">
      <h1>Personal Info</h1>
      <span>Please provide your name, email address, and phone number.</span>
    </div>

    <div class="[ form-info ]" v-for="(info, index) in infos" :key="index">
      <div class="[ validation ]">
        <label>{{ info.label }}</label>
        <span v-if="!formData[info.key] && checkValidation[index]" class="[ error ]"
          >This field is required</span
        >
      </div>
      <input
        v-model="formData[info.key]"
        type="{{ info.type }}"
        :placeholder="placeholderText(info)"
        @keyup="checkValidation[index] = false"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: 'PersonalInfo',
  props: {
    user: {
      type: Object,
      default: () => {}
    }
  },
  created() {
    this.formData = JSON.parse(JSON.stringify(this.user))
    this.checkValidation = Array.from(Array(3), () => false)
    this.$emit('beforeAction', this.handleValidation)
  },
  data() {
    return {
      infos: [
        { label: 'Name', type: 'text', placeholder: 'e.g. Stehpen King', key: 'name' },
        {
          label: 'Email Address',
          type: 'email',
          placeholder: 'e.g. stephenking@lorem.com',
          key: 'email'
        },
        { label: 'Phone Number', type: 'number', placeholder: 'e.g. +1 234 567 890', key: 'phone' }
      ],
      formData: {},
      checkValidation: []
    }
  },
  methods: {
    handleValidation() {
      const validation = Object.values(this.formData).find((attr) => !attr)
      this.$emit('inputValue', this.formData)
      Object.values(this.formData).map((value, key) => {
        if (!value) {
          this.checkValidation[key] = true
        }
      })
      return validation === undefined ?? true
    },
    placeholderText(info) {
      return info.placeholder
    }
  },
  beforeUnmount() {
    this.$emit('beforeAction', null)
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
    color: var(--marine-blue);
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

@media only screen and (max-width: 770px) {
  .top{
    h1 {
      margin-bottom: 15px;
    }

    span {
      font-size: 1.2rem;
    }
  }

  .form-info {
    input {
      margin-top: 5px;
    }
  }
}
</style>
