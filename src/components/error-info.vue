<template>
  <div class="error-info">
    <div class="error-info__icon">✖</div>
    <div class="error-info__description">{{ error }}</div>
  </div>
</template>

<script>
export default {
  props: {
    error: {
      type: String,
      default: 'Произошла ошибка'
    }
  }
}
</script>

<style lang="scss" scoped>
.error-info {
  flex: 1;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  .error-info__icon {
    border: 2px solid rgb(180, 80, 80);
    color: rgb(180, 80, 80);
    height: 50px;
    width: 50px;
    font-size: 30px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .error-info__description {
    width: 70%;
    text-align: center;
    margin-top: 10px;
  }
}
</style>
