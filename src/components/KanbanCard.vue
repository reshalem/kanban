<template>
  <div class="card">
    <div class="card-header font-weight-bold" id="kanban-header">
      {{ data.name }}
    </div>
    <div class="card-body">
      <Task v-for="(item) in data.data" :key="item.id" :item="item" :name="data.name" class="mb-4"></Task>
    </div>
  </div>
</template>

<script>
import Task from '@/components/Task.vue'

export default {
  name: 'KanbanCard',
  components: {
    Task
  },
  data: function () {
    return {}
  },
  props: ['data']
}
</script>

<style scoped>
#kanban-header {
  background-color: #f5f5dc;
}
</style>
