<template>
  <div class="container">
      <h2>My Todo List</h2>

      <!-- Input-->

  <div class="form">
    <input v-model="task" type="text"  placeholder="Enter Text" class="input">
    <button @click="submitTask" class="submitButton"> Submit</button>
  </div>

      <!--Table-->
  <table class="table table-bordered" style="margin-top: 50px;">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col" style="width: 150px;">Status</th>
      <th scope="col" style="width: 150px;">Edit</th>
      <th scope="col" style="width: 150px;">Delete</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task, index) in tasks" :key="index">

      <th scope="row">
        <span :class="{'finished': task.status === 'finished'}">
          {{task.name}}
        </span>
      </th>
      <td> 
        <span class="pointer" @click="changeStatus(index)">
          {{ task.status }}
        </span>
      </td>
      <td>
        <div class="pointer" @click="editTask(index)">
            <span class="fa fa-pen"></span>
        </div>
      </td>
      <td>
        <div class="pointer" @click="deleteTask(index)">
            <span class="fa fa-trash"></span>
        </div>
      </td>
    </tr>
    
  </tbody>
</table>
  </div>
</template>

<script>
export default {
    data() {
      return {
        task:'',
        editedTask: null,
        availableStatuses: ['to-do', 'in-progress', 'finished' ],
        tasks: [
          {
            name:'Lets start with a To-do List',
            status: 'to-do'
          }
        ]
      }
    },
    methods: {
      submitTask() {
        if(this.task.length === 0) return; 

        if(this.editedTask === null) {
        this.tasks.push({
          name: this.task,
          status: 'to-do'
        });
        }else {
          this.tasks[this.editedTask].name = this.task;
          this.editedTask = null;
        }
        this.task = '';
      },

      deleteTask(index) {
        this.tasks.splice(index, 1);
      },
      editTask(index) {
        this.task = this.tasks[index].name;
        this.editedTask = index;
      },
      changeStatus(index) {
        let newIndex = this.availableStatuses.indexOf(this.tasks[index].status)
        if (++newIndex > 2) newIndex = 0;
        this.tasks[index].status = this.availableStatuses[newIndex];
      }
    },
}
</script>

<style>
.container {
  text-align: center;
  margin-top: 50px;
}
.input {
  width: 400px;
  height: 35px;
  border-radius: 5px;
  border-width: 1px;
  border-color: grey;

}
.submitButton {
  background: pink;
  border-radius: 5px;
  border-width: thin;
  margin-left: 5px;
  
}
.form {
  display: flex;
  justify-content: center;
  margin-top: 50px;
}
.pointer {
  cursor: pointer;
}
.finished {
  text-decoration: line-through;
  text-decoration-thickness: 2px;

}
  

</style>