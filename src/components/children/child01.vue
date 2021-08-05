<template>
  <div>
    <p style="color: red">child counter:{{ counter }}</p>
    <button @click="showMsg">双向绑定{{ usernameChange }}</button>
  </div>
</template>
<script>
export default {
  props: {
    counter: {
      type: Number,
      required: true,
      default: 0,
    },
    usernameChange: {
      type: String,
    },
  },
  data() {
    return {
      // 如果要改变counter的值，在组件中单独定义一个变量
      tmpCounter: this.counter + 1,
    };
  },
  watch: {
    tmpCounter(o, n) {
      console.info(o, n);
    },
  },

  methods: {
    showMsg() {
      // .sync双向绑定，子组件更改值后，父组件值同步更改,.sync类似语法糖
      // 等价于父组件定义了回调方法：@update:username-change，然后传入新的值
      this.$emit('update:username-change', 'andyten-' + this.counter);
      //alert(this.username2);
      // 触发父级绑定的事件
      this.$emit('child-event', this.counter);
    },
  },
};
</script>
