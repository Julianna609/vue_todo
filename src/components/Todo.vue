<template>
  <div class="ui card">
    <transition name="fade">
      <div class="content" v-show="!isEditing">
        <div class="header">{{ todo.title }}</div>
        <div class="meta">{{ todo.project }}</div>
        <div class="extra content">
          <span class="right floated edit icon" v-on:click="showForm">
            <i class="edit icon"></i>
          </span>
          <span class="right floated trash icon" v-on:click="deleteTodo(todo)">
            <i class="trash icon"></i>
          </span>
        </div>
      </div>
    </transition>
    <transition name="fade">
      <div class="content" v-show="isEditing">
        <div class="ui form">
          <div class="field">
            <label>Title</label>
            <input type="text" v-model="todo.title">
          </div>
          <div class="field">
            <label>Project</label>
            <input type="text" v-model="todo.project">
          </div>
          <div class="ui two button attached buttons">
            <button class="ui basic blue button" v-on:click="hideForm(todo)">Close X</button>
          </div>
        </div>
      </div>
    </transition>
    <div
      class="ui bottom attached green basic button"
      v-show="todo.done"
      v-on:mouseover="hover = true"
      v-if="!hover"
    >Completed</div>
    <div
      class="ui bottom attached green basic button"
      v-show="todo.done"
      v-on:mouseleave="hover = false"
      v-if="hover"
      v-on:click="returnInTodo(todo)"
    >Return in todo</div>
    <div
      class="ui bottom attached red basic button"
      v-show="!todo.done"
      v-on:click="completeTodo(todo)"
    >Complete</div>
  </div>
</template>

<script>
export default {
  props: ["todo"],
  data() {
    return {
      isEditing: false,
      hover: false
    };
  },
  methods: {
    showForm() {
      this.isEditing = true;
    },
    hideForm(todo) {
      this.isEditing = false;
      this.$emit("edited-todo", todo);
    },
    deleteTodo(todo) {
      this.$emit("delete-todo", todo);
    },
    completeTodo(todo) {
      this.$emit("complete-todo", todo);
    },
    returnInTodo(todo) {
      this.$emit("return-in-todo", todo);
    }
  }
};
</script>


<style>
/* .fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
} */
</style>
