<template>
  <div class="list">
    <div class="list__item" v-for="(item, index) in items" :key="index">
      <img v-if="item.img" :src="item.img" />
      <div>
        <slot :item="item" />
        <button @click="$emit('selected', item)" class="list__button">Выбрать</button>
      </div>
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
    image: {
      type: String,
      default: null
    }
  }
}
</script>

<style lang="scss" scoped>
.list {
  overflow-y: auto;

  .list__item {
    width: 100%;
    display: flex;
    font-size: 14px;
    margin: 8px 0;

    > img {
      height: 100%;
      width: 150px;
      object-fit: cover;
    }

    > div {
      flex: 1;
      padding: 0 8px;
      display: flex;
      flex-direction: column;

      .list__button {
        background: lightcoral;
        color: white;
        border: none;
        outline: none;
        padding: 8px 20px;
        margin: auto 0 0 auto;
        border-radius: 16px;
        cursor: pointer;
      }
    }
  }
}
</style>
