<template>
  <div class="todo-item">
    <p
      v-if="!todoItem.completed">
      {{ todoTitle }}
    </p>
    <del v-else>
      {{ todoTitle }}
    </del>
    <div class="item-actions">
      <input
        type="checkbox"
        v-model="completed"
      />
      <button
        type="button"
        class="btn-delete"
        @click="$emit('on-delete', todoItem.id)">
        Delete
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TodoItem',
  props: {
    orderNumber: Number,
    todoItem: Object,
  },
  computed: {
    todoTitle() {
      return this.orderNumber + '.' + this.todoItem.title;
    },
    completed: {
      get() {
        return this.todoItem.completed;
      },
      set(value) {
        this.$emit('on-update', {id: this.todoItem.id, completed: value});
      },
    },
  },
};
</script>

<style scoped>
  .todo-item {
    display: flex;
    justify-content: space-between;
    text-align: start;
    align-items: center;
    height: 50px;
  }
  .item-actions {
    display: flex;
    align-items: center;
  }
  .item-actions input {
    margin-right: 1.25rem;
  }
  .item-actions button {
    padding: 5px 20px;
    border-radius: 4px;
    border: none;
    cursor: pointer;
  }
  .title {
    position: relative;
  }
  .title p.completed::after {
    content: '';
    width: 100%;
    border-bottom: 1px solid gray;
    position: absolute;
    left: 0;
    top: 50%;
  }
</style>
