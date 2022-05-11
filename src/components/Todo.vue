<template>
  <div class="container">
    <h2 class="text-center mt-2 text-uppercase headers">Welcome to my Todo App</h2>
    
    <!-- Form Section -->
    <div class="mt-5 d-flex justify-content-end col-md-10">
      <button class="btnsub" @click="displayForm">Add Task</button>
    </div>
    <!-- Table Section -->
    <div class="col-md-8 mx-auto">
      <p class="text-danger text-center mt-5 mystyle">{{message}}</p>
      <table class="table table-bordered mt-5">
        <thead>
          <tr class="first-row text-white col-2">
            <th scope="col" class="text-center col-4 p-2">Task</th>
            <th scope="col" class="text-center p-2">Status</th>
            <th scope="col" class="text-center p-2">Priority</th>
            <th scope="col" class="text-center p-2">Due Date</th>
            <th scope="col" class="text-center p-2">Edit</th>
            <th scope="col" class="text-center p-2">Delete</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(task, index) in bigTasks" :key="index">
            <td class="text-center">{{ task.addTask }}</td>  
            <td class="text-center">{{ task.status }}</td>  
            <td class="text-center">{{ task.priority }}</td> 
            <td class="text-center">{{ task.eta }}</td>          
            <td>
              <div class="text-center" @click="editTask(index)">
                <span class="fa fa-pen text-success"></span>
              </div>
            </td>
            <td>
              <div class="text-center" @click="deleteTask(index)">
                <span class="fa fa-trash text-danger"></span>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <div class="backdrop" v-if="showForm"> 
      <form @submit.prevent="submitTask">
        <div class="close" @click="displayForm"><i class="fa-solid fa-xmark"></i></div>
        <label>Add Task:</label>
        <input type="text" required v-model="addTask">
        
        <label>Due Date:</label>
        <input type="datetime-local" required v-model="eta" class="pointer">

        <label>Status:</label>
        <select v-model="status" required>
          <option value="Todo">Todo</option>
          <option value="In-Progress">In-Progress</option>
          <option value="Completed">Completed</option>
        </select>

        <label>Priority:</label>
        <select v-model="priority" required>
          <option value="Low">Low</option>
          <option value="Medium">Medium</option>
          <option value="High">High</option>
        </select>

        <div class="submit">
          <button class="btnsub">Add Task</button>
        </div>
      
      </form>
    </div>


  </div>
</template>

<script>
  export default {
    data(){
      return {
        showForm: false,
        addTask: '',
        status: '',
        priority: '',
        eta: '',
        bigTasks: [],
        editedTask: null,
      }
    },
    methods: {
      submitTask(){

        if(this.editedTask === null){
            this.bigTasks.push({
            addTask: this.addTask,
            status: this.status,
            priority: this.priority,
            eta: this.eta
          })
        }else {
          this.bigTasks[this.editedTask].addTask = this.addTask
          this.bigTasks[this.editedTask].status = this.status
          this.bigTasks[this.editedTask].priority = this.priority
          this.bigTasks[this.editedTask].eta = this.eta
        }

        this.showForm = false
        
        this.addTask = ''
        this.status = ''
        this.priority = ''
        this.eta = ''
      
      },

      displayForm() {
        this.showForm = !this.showForm
      },

      deleteTask(index) {
        this.bigTasks.splice(index, 1);
      },

      editTask(index) {
        this.showForm = true
  
        this.addTask = this.bigTasks[index].addTask
        this.status = this.bigTasks[index].status
        this.priority = this.bigTasks[index].priority
        this.eta = this.bigTasks[index].eta
        this.editedTask = index
      },
          
    }
   
  }
</script>

<style scoped>

  .close {
    text-align: end;
    color: rgb(250, 20, 20);
    font-size: 30px;
    padding-bottom: 0;
    cursor: pointer;
  }

  .headers {
    color: rgb(14, 1, 131);
  }
  .pointer {
    cursor: pointer;
  }
  .first-row {
    background: rgb(14, 1, 131);
  }
  .mystyle {
    font-weight: bolder;
  }
  option {
    border: 2px solid #fff;
  }

  .backdrop {
    top: 8%;
    position: fixed;
    margin: auto;
    left: 0;
    right: 0;
    width: 100%;
    height: 100%;
  }

  form {
    max-width: 430px;
    margin: 10px auto;
    background: rgb(14, 1, 131);
    text-align: left;
    padding: 10px 40px;
    border-radius: 10px;
  }
  label {
    color: #fff;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.7em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
  }
  input, select {
    display: block;
    padding: 8px 6px;
    width: 100%;
    box-sizing: border-box;
    color: #555;
  }

  .terms {
    text-align: center;
  }

  .pills {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #000;
    cursor: pointer;
  }
  .btnsub {
    cursor: pointer;
    padding: 10px 20px;
    font-size: 15px;
    background: rgb(250, 20, 20);
    border: 0;
    color: #fff;
    margin-bottom: 20px;
  }
  .submit {
    text-align: center;
    margin-top: 20px;
  }
  .error {
    color: yellow;
    font-size: 14px;
    margin-top: 10px;
    text-align: center;
  }
</style>
