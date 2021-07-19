<template>
  <div>
    <p style="color: red">child counter:{{ counter }}</p>
    <button @click="showMsg">childClick</button>
  </div>
</template>
<script>
export default {
  props: {
    counter: Number,
  },
  data() {
    return {
      // 如果要改变counter的值，在组件中单独定义一个变量
      tmpCounter: this.counter + 1,
    };
  },
  watch: {
    tmpCounter(o, n) {},
  },

  methods: {
    showMsg() {
      // 触发父级绑定的事件
      this.$emit("child-event", this.counter);
    },
  },
};
</script>>