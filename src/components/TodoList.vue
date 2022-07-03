<template>
  <div class="todo-list">
    <TodoListInsertForm
      v-model.trim="title"
      @onAddTodoItem="onAddTodoItem"
      @enter="onAddTodoItem"
    />
    <TodoItem
      v-for="(todoItem, index) in todoItems"
      :key="todoItem.id"
      :order-number="index + 1"
      :todo-item="todoItem"
      @on-update="onUpdateTodoItem"
      @on-delete="onDeleteTodoItem"
    />
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue';
import TodoListInsertForm from './TodoListInsertForm.vue';

export default {
  name: 'TodoList',
  props: {
  },
  components: {
    TodoItem,
    TodoListInsertForm,
  },
  data() {
    return {
      todoItems: [],
      title: '',
    };
  },
  created() {
    this.fetchTodoItems();
  },
  computed: {
    todoItemsLength() {
      return this.todoItems.length;
    },
  },
  methods: {
    fetchTodoItems() {
      fetch('https://jsonplaceholder.typicode.com/todos')
          .then((res) => res.json())
          .then((json) => this.todoItems = json);
    },
    onUpdateTodoItem(args) {
      const index = this.todoItems.findIndex((item) => item.id === args.id);
      if (index === -1) return;
      this.todoItems[index].completed = args.completed;
    },
    onDeleteTodoItem(id) {
      const index = this.todoItems.findIndex((item) => item.id === id);
      this.todoItems.splice(index, 1);
    },
    onAddTodoItem() {
      if (this.title.length === 0) return;

      const todoItem = {
        id: this.todoItems.length + 1,
        title: this.title,
        completed: false,
        user: 1,
      };
      this.todoItems.unshift(todoItem);
      this.title = '';
    },
  },
};
</script>

<style scoped>
@media screen and (min-width: 768px)  {
  .todo-list {
    width: 50%;
  }
}
.todo-list {
  margin: 0 auto;
  border: 1px solid gray;
  border-radius: 8px;
  padding: 20px;
}
</style>
