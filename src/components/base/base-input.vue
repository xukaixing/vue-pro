<!--
 * @Copyright: Copyright (c) 2021 andyten
 * @Description:  base-input组件
 * @Author: andy.ten@tom.com
 * @Date: 2021-08-01 21:23:31
 * @LastEditors: andy.ten@tom.com
 * @LastEditTime: 2021-08-01 23:04:17
 * @Version: 1.0.1
-->
<template>
  <label>
    {{ label }}
    <!-- <input v-bind="$attrs" :value="value" @input="$emit('input', $event.target.value)" /> -->
    <!-- <input v-bind="$attrs" :value="value" @input="inputDefault" /> -->
    <input v-bind="$attrs" v-on="inputListeners" :value="value" />
    - {{ value }}
  </label>
</template>
<script>
export default {
  // 对于非props的attribute，不希望组件的根元素（label）继承 attribute，在组件的选项中设置 inheritAttrs: false
  // inheritAttrs选项不会影响 style 和 class 的绑定，style和class是合并
  // 这种做法可以使组件直接使用input的基本属性，而不用担心input是不是根组件。
  inheritAttrs: false,
  // v-model默认绑定的是属性value和事件input
  model: {
    prop: 'value',
    event: 'input',
  },
  props: {
    label: {
      type: String,
      required: true,
    },
    value: {
      type: String,
      default: '',
    },
  },
  computed: {
    inputListeners: function() {
      var vm = this;
      // `Object.assign` 将所有的对象合并为一个新对象
      return Object.assign(
        {},
        // 我们从父级添加所有的监听器
        this.$listeners,
        // 然后我们添加自定义监听器，
        // 或覆写一些监听器的行为
        {
          // 这里确保组件配合 `v-model` 的工作
          input(event) {
            vm.$emit('input', event.target.value);
          },
          // 此处如果自定义监听器，将会覆盖父级定义的监听器
          // blur() {
          //   alert(1);
          // },
        }
      );
    },
  },
  methods: {
    inputDefault(event) {
      this.$emit('input', event.target.value);
    },
  },
};
</script>
