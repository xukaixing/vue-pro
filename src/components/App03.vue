<template id="app-3">
  <div id="app-3">
    <p
      class="header-title"
      :style="{ fontSize: 18 + 'px', fontWeight: 'bold' }"
    >
      {{ "App03" + ":" + message3 }}
    </p>
    <ul>
      <li v-for="(todo, index) in todos" :key="todo.id">
        序号：{{ index }} - {{ todo.text }}
      </li>
    </ul>
    <p>-遍历对象属性，调试时使用该方式可遍历对象内容</p>
    <ul>
      <li v-for="(value, key) in obj" :key="key">{{ key }} - {{ value }}</li>
    </ul>
    <p
      class="header-title"
      :style="{ fontSize: 18 + 'px', fontWeight: 'bold' }"
    >
      {{ message4 }}
    </p>
    <ol>
      <!-- Now we provide each todo-item with the todo object    -->
      <!-- it's representing, so that its content can be dynamic -->
      <!-- 静态参数和动态参数 -->
      <todo-item
        v-for="item in groceryList"
        :todo="item"
        :key="item.id"
        title="todoitems"
      ></todo-item>
    </ol>
  </div>
</template>

<script>
// 局部作用域组件定义
const todoItem = {
  props: ["todo", "title"],
  // 组件被多次引用时，是使用相同的选项，所以data必须是函数保证组件被多次引用时互相不受影响。
  data() {
    return {
      message: "Component",
    };
  },
  template: "<li>[{{title}}]:{{ message }}:{{ todo.text }}</li>",
};
export default {
  name: "app03",
  data() {
    return {
      message3: "v-for",
      todos: [
        {
          text: "Learn JavaScript",
          id: "1",
        },
        {
          text: "Learn Vue",
          id: "2",
        },
        {
          text: "Build something awesome",
          id: "3",
        },
      ],
      obj: {
        id: "1",
        name: "hello",
        value: "world",
      },
      message4: "component",
      groceryList: [
        {
          text: "Vegetables",
          id: 1,
        },
        {
          text: "Cheese",
          id: 2,
        },
        {
          text: "Whatever else humans are supposed to eat",
          id: 3,
        },
      ],
    };
  },
  // 局部组件定义
  components: {
    todoItem,
  },
};
</script>