<template id="app-1">
  <div id="app-1">
    <p
      class="header-title"
      :style="{ fontSize: 18 + 'px', fontWeight: 'bold' }"
    >
      {{ "App01" + ":" + message }}
    </p>
    <input v-model="message" placeholder="helloworld" />
    <p>{{ message2 }}</p>
    <p />
    <textarea v-model="textareamgs" placeholder="enter textarea"></textarea>

    <p>{{ textareamgs }}</p>
  </div>
</template>

<script>
export default {
  name: "app01",
  data() {
    return {
      message: "Hello Vue!",
      message2: "Hello Vue2!",
      textareamgs: "Hello Vue Textarea",
    };
  },
  // vue实例创建后钩子-hook
  created() {
    this.$data.message = "Hello Vue Hook!";
  },
};
// 该属性是在创建前代理的，所以该属性是响应的
//app1.message='hello Vue1';
// 创建vue实例后添加新的属性,该属性是非响应的
//app1.addNewPro='hello Vue3';
</script>