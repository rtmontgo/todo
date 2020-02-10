<template>
 <div>
  <div class="viewport">
      <md-toolbar class="md-accent" :md-elevation="3">
        <span class="md-title">Do The Things</span>
      </md-toolbar>
      </div>
  
  <md-field>
      <md-input v-model="currentTodo" @keydown.enter="addTodo()" placeholder="Add a todo"></md-input>
    </md-field>

    <md-empty-state
     class="md-accent"
      md-icon="devices_other"
      md-label="You have nothing todo"
      md-description="Create a todo and get to  work."
      v-if="todos.length === 0">
    </md-empty-state>
    
 <ul class="todos">
  <li v-for="todo in todos" :key="todo.id">
  
 <md-field>
 <input class ='completeButton' type='checkbox' v-model="todo.completed">
  <span
              class="todo-item-label"
              :class='{completed: todo.completed}' 
              @dblclick='editTodo(todo)' 
              v-if="!todo.edit">
                {{todo.label}}
              </span>
              
              <md-input v-else class="todo-item-edit" 
              type="text" v-model='todo.label'
              @keyup.enter="completedEdit(todo)"
              placeholder="Edit your task"> 
              </md-input>
            
   <button @click="removeTodo(todo)">Delete</button>
   </md-field>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'EmptyStateBasic',
  data() {
    return {
      todos: [],
      currentTodo: '',
      editedTodo: null
    };
  },
  methods: {
    addTodo() {
      this.todos.push({id: this.todos.length, label: this.currentTodo, completed: false, edit: false});
      this.currentTodo = '';
      },
    editTodo(todo) {
      todo.edit = true;
    },
    completedEdit(todo) {
      todo.edit = false;
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    }
    }
  };
</script>

<style>
.md-toolbar {
  justify-content: center;
  align-items: center;
}
.todo-item-label {
  padding: 0 20px;
}
  .completed {
  text-decoration: line-through;
  }

  .closeButton {
  float: right;
}
.closeButton:hover {
  cursor: pointer;
  transition: 0.2s ease;
    color: red
}
.completeButton {
  float: left;
  margin-left: 15px;
}

</style>
