<template>
  <list v-slot:default="{ item }" :items="times" @selected="$emit('selected', $event)">
    <div>{{ item | moment('Do MMMM в h:mm') }}</div>
  </list>
</template>

<script>
export default {
  components: {
    List: () => import('@/components/list')
  },
  props: {
    times: {
      type: Array,
      required: true
    }
  }
}
</script>
