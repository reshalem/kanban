<template>
  <div class="card">
    <div class="card-header font-weight-bold" id="content-header">
      {{ item.title }}
    </div>
    <div class="card-body text-left">
      <div class="font-weight-bold">
        Description:
        <p class="lead">{{ item.description }}</p>
      </div>
      <div class="font-weight-bold">
        Point:
        <p class="lead">{{ item.point }}</p>
      </div>
      <div class="font-weight-bold">
        Assigned To:
        <p class="lead">{{ item.assigned_to }}</p>
      </div>
    </div>
    <div class="card-footer">
      <button class="btn btn-danger btn-block font-weight-bold mb-2" id="btn-delete" data-toggle="modal" data-target="#confirmModalDelete">Delete</button>
      <div class="modal fade mt-5" id="confirmModalDelete">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-body">
              <div class="mb-4 mt-3">Are you sure you want to delete this task?</div>
              <div class="mb-3">
                <button class="btn btn-danger font-weight-bold" data-dismiss="modal">Cancel</button>
                <button class="btn btn-primary font-weight-bold ml-5" data-dismiss="modal" @click="removeItem">Positive</button>
              </div>
            </div>
          </div>
        </div>
      </div>
      <button class="btn btn-block font-weight-bold" id="btn-one" v-if="buttonOne" @click="moveUp">{{ buttonOne }}</button>
      <button class="btn btn-block font-weight-bold" id="btn-two" @click="moveDown" v-if="buttonTwo">{{ buttonTwo }}</button>
    </div>
  </div>
</template>

<script>
import database from '../assets/config.js'

export default {
  name: 'ContentCard',
  data: function () {
    return {
      buttonOne: '',
      buttonTwo: ''
    }
  },
  props: ['item', 'name'],
  methods: {
    moveUp: function () {
      database.ref(`/${this.item.id}`).remove()
      database.ref('/').push({
        title: this.item.title,
        description: this.item.description,
        point: this.item.point,
        assigned_to: this.item.assigned_to,
        status: this.buttonOne
      })
    },
    moveDown: function () {
      database.ref(`/${this.item.id}`).remove()
      database.ref('/').push({
        title: this.item.title,
        description: this.item.description,
        point: this.item.point,
        assigned_to: this.item.assigned_to,
        status: this.buttonTwo
      })
    },
    removeItem: function () {
      database.ref(`/${this.item.id}`).remove()
    }
  },
  created () {
    if (this.name === 'Back-Log') {
      this.buttonOne = 'To-Do'
      this.buttonTwo = null
    } else if (this.name === 'To-Do') {
      this.buttonOne = 'Doing'
      this.buttonTwo = 'Back-Log'
    } else if (this.name === 'Doing') {
      this.buttonOne = 'Done'
      this.buttonTwo = 'To-Do'
    } else {
      this.buttonOne = null
      this.buttonTwo = 'Doing'
    }
  }
}
</script>

<style scoped>
#btn-one {
  background-color: #008080;
  color: white;
  border: none !important;
  border-color: #cccccc;
  -webkit-box-shadow: none;
  box-shadow: none;
}

#btn-two {
  background-color: #ffa500;
  color: white;
  border: none !important;
  border-color: #cccccc;
  -webkit-box-shadow: none;
  box-shadow: none;
}

#btn-delete {
  border: none !important;
  border-color: #cccccc;
  -webkit-box-shadow: none;
  box-shadow: none;
}

#content-header {
  background-color: #3b5998;
  color: white;
}
</style>
