<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoFooter>
      <p slot="text">clear all</p>
    </TodoFooter>
    <TodoInput v-on:save="addTodoItem"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" v-on:remove="removeTodoItem"></TodoList>
    <TodoFooter v-on:clear="clearTodoItems">
      <p slot="text">clear all</p>
      <i slot="icon" class="fas fa-dumpster"></i>
    </TodoFooter>
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";
import TodoFooter from "./components/TodoFooter.vue";

export default {
  components: {
    TodoHeader: TodoHeader,
    TodoInput: TodoInput,
    TodoList: TodoList,
    TodoFooter: TodoFooter
  },

  data() {
    return {
      todoItems: []
    };
  },

  methods: {
    addTodoItem(todoItem) {
      // 할 일 데이터 배열에 '새 할 일' 추가
      this.todoItems.push(todoItem);
      // 저장소(DB)에 새 데이터 추가
      localStorage.setItem(todoItem, todoItem);
    },
    removeTodoItem(todoItem, index) {
      // 뷰의 데이터 배열에서 삭제
      this.todoItems.splice(index, 1);
      // 데이터 저장소에서 데이터 삭제
      localStorage.removeItem(todoItem);
    },
    clearTodoItems() {
      // 전체삭제
      this.todoItems = [];
      localStorage.clear();
    }
  },

  created() {
    if (localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
          this.todoItems.push(localStorage.key(i));
        }
      }
    }
  }
};
</script>

<style>
@import url("./assets/css/common.css");
</style>
