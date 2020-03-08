<template>
  <list v-slot:default="{ item }" :items="workers" @selected="$emit('selected', $event)">
    <div><b>ФИО:</b> {{ item.fio }}</div>
    <div><b>Описание:</b> {{ item.description }}</div>
  </list>
</template>

<script>
export default {
  components: {
    List: () => import('@/components/list')
  },
  props: {
    workers: {
      type: Array,
      required: true
    }
  }
}
</script>
