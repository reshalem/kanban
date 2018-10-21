<template>
  <div class="mt-4">
    <h1 class="h1 mb-4" id="kanban-title">~|~ Kanban ~|~</h1>
    <button class="btn btn-dark font-weight-bold mb-5" id="btn-newTask" data-toggle="modal" data-target="#inputModal">New Task</button>

    <div class="modal fade" id="inputModal">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
              <h5 class="modal-title">New Task</h5>
              <button class="close" data-dismiss="modal">&times;</button>
          </div>
          <div class="modal-body">
            <form>
              <div class="form-group d-flex flex-column">
                  <label for="title" class="text-left">Title</label>
                  <input type="text" placeholder="Task Title" class="form-control" v-model="task.taskName">
              </div>
              <div class="form-group d-flex flex-column">
                  <label for="description" class="text-left">Description</label>
                  <textarea class="form-control" id="message" rows="3" placeholder="Task Brief Explanation" v-model="task.description"></textarea>
              </div>
              <div class="form-group d-flex flex-column">
                  <label for="point" class="text-left">Point</label>
                  <input type="text" placeholder="0" class="form-control" v-model="task.point">
              </div>
              <div class="form-group d-flex flex-column">
                  <label for="assigned-to" class="text-left">Assigned To</label>
                  <input type="text" placeholder="Assigned To" class="form-control" v-model="task.assigned_to">
              </div>
            </form>
          </div>
          <div class="modal-footer ">
              <button class="btn btn-danger font-weight-bold" data-dismiss="modal">Cancel</button>
              <button class="btn btn-primary font-weight-bold ml-1" data-dismiss="modal" @click="sendItem">Create</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import database from '../assets/config.js'

export default {
  name: 'Header',
  data: function () {
    return {
      task: {
        taskName: '',
        description: '',
        point: '',
        assigned_to: ''
      }
    }
  },
  methods: {
    sendItem: function () {
      database.ref('/').push({
        title: this.task.taskName,
        description: this.task.description,
        point: this.task.point,
        assigned_to: this.task.assigned_to,
        status: 'Back-Log'
      })
      this.task = {}
    }
  }
}
</script>

<style scoped>
#kanban-title {
  font-family: 'Roboto Slab', serif !important;
}

#btn-newTask {
  border: none !important;
  border-color: #cccccc;
  -webkit-box-shadow: none;
  box-shadow: none;
}
</style>
