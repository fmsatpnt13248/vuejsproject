<script>
export default {
    data() {
        return {
            newTodo: '',
            todoID: 0,
            todos: {},
            editIndex: null,
            editTodo: ''
        }
    },
    methods: {
        addTodo: function() {
            if (this.newTodo !== '') {
                this.todoID++;
                this.todos[this.todoID] = this.newTodo;
                // this.todos.push(this.newTodo);
                this.newTodo = '';
            }
        },
        // removeTodo: function(index) {
        //     this.$delete(this.todos, index);
        //     this.editIndex = null;
        // },
        editTodoItem: function(index) {
            this.editIndex = index;
            this.editTodo = this.todos[index];
        },
        saveEdit: function(index) {
            if (this.editTodo !== '') {
                this.todos[index] = this.editTodo;
                this.editIndex = null;
                this.editTodo = '';
            }
        }
    }
};
</script>

<template>
    <h1 class="text-center mb-4">To-Do List</h1>

    <div class="input-group mb-3">
        <input v-model="newTodo" placeholder="Add a new to-do" type="text" class="form-control"/>

        <div class="input-group-append">
            <button @click="addTodo" class="btn btn-primary">Add</button>
        </div>
    </div>

    <ul class="list-group">
        <li v-for="(todo, index) in todos" :key="index" class="list-group-item d-flex justify-content-between align-items-center">
            <div v-if="editIndex === index" class="flex-grow-1 mr-3">
                <input v-model="editTodo" @keyup.enter="saveEdit(index)" class="form-control"/>
            </div>
            <div v-else class="flex-grow-1">
                {{ todo }}
            </div>

            <div>
                <button v-if="editIndex === index" @click="saveEdit(index)" class="btn btn-success btn-sm mr-2">
                    Save
                </button>
                <button v-else @click="editTodoItem(index)" class="btn btn-warning btn-sm mr-2" >
                    Edit
                </button>
                <button @click="delete todos[index]" class="btn btn-danger btn-sm">
                    Remove
                </button>
            </div>
        </li>
    </ul>
</template>
