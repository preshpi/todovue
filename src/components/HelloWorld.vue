<template>
    <div class="container">
      <div>
        <h4 class="bg-primary text-white text-center p-2">{{name}}'s' TODO List</h4>
      </div>
      <div class="container-fluid p-4 m-4">
          <div class="row" v-if="filteredTasks.length == 0">
          <div class="col text-center">
            <b>Nothing to do. Hurray!!</b>
          </div>
          </div>
    
          <div v-else>
            <div class="row">
              <div class="col font-weigth-bold mb-3">Task</div>
              <div class="col-2 font-weigth-bold mb-3">Done</div>
            </div>
          </div>

        <div class="row" v-for="task in filteredTasks" :key="task.action" >
          <div class="col">
            {{ task.action }}
          </div>
      
          <input type="checkbox" v-model="task.done" class="form-check-input"/>
          <div class="col-2">{{ task.done }}</div>
        </div>

        <div class="row py-2 container">
          <div class="col">
            <input type="text" v-model="newItem" class="form-control"/>     
          </div>
          
          <div class="col-2">
            <button class="btn btn-primary" v-on:click="addNewTodo">Add</button>
          </div>
        </div>

        <div class="row bg-secondary py-2 mt-2 text-white container">
          <div class="col text-center">
            <input type="checkbox" v-model="hideCompleted" class="form-check-input">
            <label for="HideTask" class="form-check-label font-weight-bold">
              Hide completed Task
            </label>
              <div class="">      
                 <button class="btn btn-sm btn-danger" v-on:click="deleteCompleted">Delete</button>
               </div>
        </div>
        
        </div>
      </div>
    </div>
</template>

<script>
export default {
   name: 'app',
   data () { return {
      name: 'Precious',
      tasks: [
        {action: 'Buy Flowers', done:true},
        {action: 'Call Joe', done:false},
        {action: 'Pick sister', done:true},
        {action: 'Read book', done:false},
      ],
      hideCompleted: true,
      newItem: ' '

    }
   },
   computed: {
    filteredTasks () {
      return this.hideCompleted ? this.tasks.filter(task => !task.done) : this.tasks    
    }

    },
    methods: {
      addNewTodo () {
        this.tasks.push({
          action: this.newItem,
          done: false
        })
        localStorage.setItem('todos', JSON.stringify(this.tasks))
        this.newItem = ''
      },
      storeData () { 
        localStorage.setItem('todos', JSON.stringify(this.tasks))
      },
      deleteCompleted () { 
        this.tasks =  this.tasks.filter(task => !task.done)
        
        }
    },
    created () {
      const data = localStorage.getItem('todos')
      if (data != null) {
        this.tasks = JSON.parse(data)
      }
    }
   }
  

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
