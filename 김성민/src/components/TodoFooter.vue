<template>
  <div class="clearAllContainer">
    <span class="clearAllBtn" @click="clearAll">
      <slot name="text"></slot>
      <slot name="icon"></slot>
    </span>
  </div>
</template>

<script>
import { bus } from "../utils/bus.js";

export default {
  methods: {
    clearAll: function() {
      // 이벤트 버스로 이벤트 보내기
      this.$emit("clear");
    }
  }
};
</script>

<style scoped>
.clearAllContainer {
  width: 8.5rem;
  height: 50px;
  line-height: 50px;
  background-color: white;
  border-radius: 5px;
  margin: 0 auto;
}
.clearAllBtn {
  color: #e20303;
  display: block;
}
</style>
