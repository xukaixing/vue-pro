<!--
 * @Copyright: Copyright (c) 2021 andyten
 * @Description:  base-input组件
 * @Author: andy.ten@tom.com
 * @Date: 2021-08-01 21:23:31
 * @LastEditors: andy.ten@tom.com
 * @LastEditTime: 2021-08-01 22:48:06
 * @Version: 1.0.1
-->
<template>
  <label>
    {{ label }}
    <input type="checkbox" :checked="checked" @change="checkboxChange" />
    - {{ checked }}
    <p />
    value:{{ value }}
  </label>
</template>
<script>
export default {
  // 一个组件上的 v-model 默认会利用名为 value 的 prop 和名为 input 的事件
  // 但是像单选框、复选框等类型的输入控件可能会将 value attribute 用于不同的目的
  // model 选项可以用来避免这样的冲突,自定义组件的prop和event，而不是默认的value和input事件
  model: {
    prop: 'checked',
    event: 'change',
  },
  props: {
    checked: {
      type: Boolean,
      required: true,
    },
    value: {
      type: String,
      default: '',
    },
  },
  methods: {
    checkboxChange(event) {
      this.$emit('change', event.target.checked);
    },
  },
};
</script>
