<template>
  <div class="user-form">
    <div>Введите ФИО и Телефон</div>
    <input v-model="user.fio" :class="!validateFio ? 'invalid' : ''" @input="$emit('input', user)" type="text" placeholder="ФИО" />
    <input v-model="user.phone" :class="!validatePhone ? 'invalid' : ''" @input="$emit('input', user)" type="text" placeholder="Телефон" />
    <button class="user-form__button" @click="validate">Записаться</button>
  </div>
</template>

<script>
export default {
  model: {
    prop: 'data',
    event: 'input'
  },
  props: {
    data: {
      type: Object,
      required: true
    }
  },
  data: () => ({
    user: {
      fio: '',
      phone: ''
    }
  }),
  computed: {
    validateFio() {
      return this.data.fio.split(' ').length > 1
    },
    validatePhone() {
      return this.data.phone.length == 12
    },
    validateAll() {
      return this.validateFio && this.validatePhone
    }
  },
  methods: {
    validate() {
      if (this.validateAll) {
        this.$emit('selected')
      }
    }
  },
  watch: {
    data: {
      handler(val) {
        this.user = val
      },
      immediate: true
    }
  }
}
</script>

<style lang="scss" scoped>
.user-form {
  flex: 1;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  input {
    padding: 8px 20px;
    border-radius: 16px;
    border: 1px solid rgb(209, 209, 209);
    margin-top: 8px;
    outline: none;

    &.invalid {
      border: 1px solid lightcoral;
    }
  }

  button {
    background: lightcoral;
    color: white;
    border: none;
    outline: none;
    padding: 8px 20px;
    margin-top: 8px;
    border-radius: 16px;
    cursor: pointer;
  }
}
</style>
