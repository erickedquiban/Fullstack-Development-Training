<template>
  <div id="q-app">
    <div class="container">
      <Header @toggle-add-task="toggleAddTask" title="TT" 
      :showAddTask="showAddTask" />
      <div v-if="showAddTask">
      <AddTask @add-task="addTask" />
      </div>
      <Tasks
        @toggle-reminder="toggleReminder"
        @delete-task="deleteTask"
        :tasks="tasks"
      />
    </div>
  </div>
</template>
<script>
import Header from "./components/header";
import Tasks from "./components/Tasks";
import AddTask from "./components/Addtask";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask
  },
  data() {
    return {
      tasks: [],
      showAddTask: false
    };
  },

  methods: {
    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    },
   async addTask(task) {
       const res = await fetch('http://localhost:5000/tasks' , {
         method: 'POST',
        //  post is for add and create 
         headers:{
           'Content-type' : 'application/json',
         },
         body: JSON.stringify(task),
       })
       const data = await res.json()
      //  response here
        this.tasks = [...this.tasks, data];
        // all data from array
    },

   async deleteTask(id) {
      if (confirm("Are you sure?")) {
        const res = await fetch(`http://localhost:5000/tasks/${id}`, {
          method: 'DELETE',
        })
        res.status === 200 
        ? (this.tasks = this.tasks.filter(task => 
        task.id !== id)) 
        : alert ('Error Deleting Task')
      }
    },

  async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id)
      const uptTask = {...taskToToggle , reminder : !taskToToggle.reminder}

      const res = await fetch(`http://localhost:5000/tasks/${id}`, {
        method: 'PUT',
        headers:{
          'Content-type' : 'application/json'
        },
        body: JSON.stringify(uptTask)
     })

      const data = await res.json()

      this.tasks = this.tasks.map(task = task.id === id ?
       {...task, reminder: data.reminder } : task
      );
    },

    async fetchTasks() {
      const res= await fetch ('http://localhost:5000/tasks')

      const data  = await res.json()

      return data
      // this is how call the array
    },

    async fetchTask(id) {
      const res= await fetch (`http://localhost:5000/tasks/${id}`)

      const data  = await res.json()

      return data
      // fetching specific task
    }
  },

   async created() {
    this.tasks = await this.fetchTasks()
    // life hook for calling entering the page
      
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Poppins", sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
