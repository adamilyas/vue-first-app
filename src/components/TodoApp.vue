<template>
  <div class="container">
    <h1 class="text-center mt-5"></h1>

    <!-- INPUT -->
    <div class="d-flex">
      <input v-model="task" type="text" class="form-control" placeholder="Enter Task">
      <button @click="submitTask" class="btn btn-warning rounded-0">SUBMIT</button>
    </div>

    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col">#</th>
          <th scope="col">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>
            <div v-if="task.isEditting">
              <input type="text" class="form-control" :placeholder=task.name v-model="newTask" v-on:keyup.enter="updateTask(newTask, index)">
            </div>
            <div v-else>{{task.name}}</div>
          </td>
          <td>{{task.status}}</td>
          <td >
            <button class="btn btn-primary" @click="toggleEditTask(index)">EDIT</button>
          </td>
          <td class="fw-bolder">
            <button class="btn btn-danger" @click="deleteTask(index)">DELETE</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },

  data(){
    return {
      tasks: []
    }
  },

  methods: {
    submitTask(){
      this.tasks.push({
        name: this.task,
        status: "todo",
      })
    },
    toggleEditTask(index){
      this.tasks[index].isEditting = !this.tasks[index].isEditting
    },
    updateTask(newTask, index){
      this.tasks[index].name = newTask
      this.tasks[index].isEditting = false
    },
    deleteTask(index){
      this.tasks.splice(index, 1)
    }
  }
}
</script>

<style scoped>
</style>
