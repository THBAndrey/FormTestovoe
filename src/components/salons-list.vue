<template>
  <list v-slot:default="{ item }" :items="salons" @selected="$emit('selected', $event)">
    <div><b>Адрес:</b> {{ item.address }}</div>
    <div><b>Время работы:</b> с {{ item.time.start }} по {{ item.time.end }}</div>
  </list>
</template>

<script>
export default {
  components: {
    List: () => import('@/components/list')
  },
  props: {
    salons: {
      type: Array,
      required: true
    }
  }
}
</script>
