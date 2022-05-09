<template>
  <div class="container">
    <h2 class="text-center mt-2 text-uppercase">Welcome to my Todo App</h2>
    
    <div class="d-flex col-md-4 mx-auto mt-5">
      <input type="text" placeholder="Enter Task" class="form-control" v-model="task">
      <button class="btn btn-warning rounded-0" @click="submitTask">Submit</button>
    </div>
    <!-- Table Section -->
    
    <div class="col-md-6 mx-auto">
      <p class="text-danger text-center mt-5 mystyle">{{message}}</p>
      <table class="table table-bordered mt-5">
        <thead>
          <tr class="first-row text-white col-2">
            <th scope="col" class="text-center">Task</th>
            <th scope="col" class="text-center">Status</th>
            <th scope="col" class="text-center">Priority</th>
            <th scope="col" class="text-center">Edit</th>
            <th scope="col" class="text-center">Delete</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(task, index) in tasks" :key="index">
            <th class="text-center">{{ task.name }}</th>
            <!-- <td class="text-center"><span class="pointer" @click="changeStatus(index)"> {{ task.status}} </span></td> -->
            <td class="text-center myBorder"><select required>
                  <option value="Developer">Todo</option>
                  <option value="Designer">In-Progress</option>
                  <option value="Designer">Completed</option>
                </select>
            </td>
            <td class="text-center"><select required>
                  <option class="myBorder">1</option>
                  <option class="myBorder">2</option>
                  <option class="myBorder">3</option>
                </select>
            </td>
            <!-- <td class="text-center"><span class="pointer" @click="changePriority(index)"> {{ task.priority }}</span></td> -->
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

  </div>
</template>

<script>
  export default {
    data(){
      return {
        task: '',
        editedTask: null,
        availableStatuses: ['to-do', 'In-progress', 'Finished'],
        priority: [1, 2, 3],
        message: '',
        tasks: [
          // {
          //   name: 'Complete My todo List App',
          //   status: 'Todo'
          // },
          //  {
          //   name: 'I will build a complete Vue App',
          //   status: 'In progress'
          // },
          //  {
          //   name: 'I will go to the office tomorrow',
          //   status: 'To do'
          // }
        ]
      }
    },
    methods: {
      submitTask(){
        this.message = '1 Is the Highest Priority and 3 is the Least. Click on Priority to Change'
        if(this.task.length === 0) return;

          if(this.editedTask === null) {
            this.tasks.push({
              name: this.task,
              status: 'to-do',
              priority: 1
            })
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
        this.editedTask = index
      },

      changeStatus(index) {
        let newIndex = this.availableStatuses.indexOf(this.tasks[index].status)
        if(++newIndex > 2) newIndex = 0
        this.tasks[index].status = this.availableStatuses[newIndex]
      },

      changePriority(index) {
        let newPriority = this.priority.indexOf(this.tasks[index].priority)
        if(++newPriority > 2) newPriority = 0
        this.tasks[index].priority = this.priority[newPriority]
      }
          
    }
   
  }
</script>

<style scoped>
  .pointer {
    cursor: pointer;
  }
  .first-row {
    background: rgb(2, 134, 90);
  }
  .mystyle {
    font-weight: bolder;
  }
  option {
    border: 2px solid #fff;
    /* width: 100%; */
  }

</style>
