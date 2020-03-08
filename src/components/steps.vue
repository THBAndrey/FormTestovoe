<template>
  <div class="steps">
    <div class="steps__item" :class="[index == active ? 'active' : '', index < active ? 'completed' : '']" v-for="(item, index) in items" :key="index">
      <div class="steps__index">
        <span v-if="index < active">✔</span>
        <span v-else>{{ index + 1 }}</span>
      </div>
      <span class="steps__description">{{ item }}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    items: {
      type: Array,
      required: true
    },
    active: {
      type: Number,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
.steps {
  height: 70px;
  width: 100%;
  display: flex;
  align-items: center;
  box-shadow: 0 1px 5px #b1b1b1;

  > .steps__item {
    flex-grow: 1;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    font-size: 14px;
    line-height: 14px;
    font-weight: 500;
    color: #363636;

    > .steps__index {
      border: 2px solid #363636;
      height: 25px;
      width: 25px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    > .steps__description {
      margin-top: 5px;
    }

    &.active {
      background-color: lightcyan;
    }

    &.completed {
      background-color: lightgreen;
    }
  }
}
</style>
