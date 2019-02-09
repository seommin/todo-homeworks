<template>
  <div>
    <ul>
      <li v-for="(todoItem, index) in propsdata" v-bind:key="todoItem" class="shadow">
        <!-- <i
          class="checkBtn fas fa-check"
          v-bind:class="{checkBtnCompleted: todoItem.completed}"
          v-on:click="toggleComplete(todoItem, index)"
        ></i>-->
        {{ todoItem }}
        <!-- <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem }}</span> -->
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
import { bus } from "../utils/bus.js";

export default {
  props: ["propsdata"],

  data() {
    return {
      todoItems: []
    };
  },

  methods: {
    removeTodo: function(todoItem, index) {
      this.$emit("remove", todoItem, index);
    }
    // toggleComplete: function(todoItem, index) {
    //   todoItem.completed = !todoItem.completed;
    //   localStorage.removeItem(todoItem.item);
    //   localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    // }
  }
  // 인스턴스 라이프 싸이클 훅
  // beforeMount: function() {
  //   // 1
  //   var vm = this;
  //   bus.$on("clear", function() {
  //     vm.clearItems();
  //   });

  //   // 2 - ES6 문법
  //   // bus.$on("clear", () => this.clearItems());
  // },
  // beforeDestroy: function() {
  //   bus.$off("clear");
  // }
};
</script>


<style scoped>
ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}

.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}

.checkBtnCompleted {
  color: #b3adad;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}

.list-enter-active,
.list-leave-active {
  transition: all 1s;
}
.list-enter,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>
