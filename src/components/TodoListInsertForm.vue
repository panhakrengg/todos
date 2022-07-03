<template>
  <div class="todo--insert">
    <input
      class="form-control"
      :value="value"
      @input="$emit('input', $event.target.value)"
      @keyup.enter="$emit('enter', $event.target.value)"
      placeholder="Add todo item"
    />
    <button
      :disabled="disabledButton"
      type="button"
      @click="$emit('onAddTodoItem')">
      Add
    </button>
  </div>
</template>

<script>
export default {
  name: 'TodoListInsertForm',
  props: {
    value: String,
  },
  computed: {
    disabledButton() {
      return this.value.length === 0;
    },
  },
};
</script>

<style scoped>
.todo--insert {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}
.todo--insert button {
  width: 15%;
  background-color: aquamarine;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
.todo--insert .form-control {
  width: 75%;
  padding: 10px 20px;
}
</style>
