<template>
  <div class="success-info">
    <div class="success-info__icon">✔</div>
    <div class="success-info__description">{{ master }} ожидает вас {{ time | moment('Do MMMM в h:mm') }} по адресу {{ salon }}</div>
  </div>
</template>

<script>
export default {
  props: {
    master: {
      type: String,
      required: true
    },
    salon: {
      type: String,
      required: true
    },
    time: {
      type: String,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
.success-info {
  flex: 1;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  .success-info__icon {
    border: 2px solid rgb(80, 180, 80);
    color: rgb(80, 180, 80);
    height: 50px;
    width: 50px;
    font-size: 30px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .success-info__description {
    width: 70%;
    text-align: center;
    margin-top: 10px;
  }
}
</style>
