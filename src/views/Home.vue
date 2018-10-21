<template>
  <div class="container">
    <Header></Header>
    <div class="card-columns col-14">
      <KanbanCard v-for="(data, index) in taskLists" :key="index" :data="data"></KanbanCard>
    </div>
  </div>
</template>

<script>
import Header from '@/components/Header.vue'
import KanbanCard from '@/components/KanbanCard.vue'

import database from '../assets/config.js'

const taskData = [
  {
    name: 'Back-Log',
    data: []
  },
  {
    name: 'To-Do',
    data: []
  },
  {
    name: 'Doing',
    data: []
  },
  {
    name: 'Done',
    data: []
  }
]

var leadsRef = database.ref('/')
leadsRef.on('value', function (snapshot) {
  taskData[0].data = []
  taskData[1].data = []
  taskData[2].data = []
  taskData[3].data = []
  snapshot.forEach(function (childSnapshot) {
    if (childSnapshot.val().status === 'Back-Log') {
      const obj = childSnapshot.val()
      obj.id = childSnapshot.key
      taskData[0].data.push(obj)
    } else if (childSnapshot.val().status === 'To-Do') {
      const obj = childSnapshot.val()
      obj.id = childSnapshot.key
      taskData[1].data.push(obj)
    } else if (childSnapshot.val().status === 'Doing') {
      const obj = childSnapshot.val()
      obj.id = childSnapshot.key
      taskData[2].data.push(obj)
    } else {
      const obj = childSnapshot.val()
      obj.id = childSnapshot.key
      taskData[3].data.push(obj)
    }
  })
})

export default {
  name: 'home',
  components: {
    Header,
    KanbanCard
  },
  data: function () {
    return {
      taskLists: taskData
    }
  }
}
</script>

<style>

</style>
