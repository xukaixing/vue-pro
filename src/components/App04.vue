<template id="app-4">
  <div id="app-4">
    <p
      class="header-title"
      :style="{ fontSize: 18 + 'px', fontWeight: 'bold' }"
    >
      App04: v-model
    </p>
    <div id="todo-list-example">
      <input
        v-model="newTodoText"
        @keyup.enter="addNewTodo"
        placeholder="Add a todo"
      />
      <ul>
        <li
          is="todo-item"
          v-for="(todo, index) in todos"
          :title="todo.text"
          :key="todo.id"
          @remove="todos.splice(index, 1)"
        ></li>
      </ul>
    </div>

    <div id="checkbox-input-example">
      <p :style="{ fontWeight: 'bold' }">{{ "checkbox example" }}</p>
      <input type="checkbox" id="ck01" value="Jack" v-model="checkedNames" />
      <label for="jack">Jack</label>
      <input type="checkbox" id="ck02" value="John" v-model="checkedNames" />
      <label for="john">John</label>
      <input type="checkbox" id="ck03" value="Mike" v-model="checkedNames" />
      <label for="mike">Mike</label>
      <br />
      <span>Checked names: {{ checkedNames }}</span>
    </div>

    <div id="radio-input-example">
      <p :style="{ fontWeight: 'bold' }">{{ "radio example" }}</p>
      <input type="radio" id="one" value="One" v-model="picked" />
      <label for="one">One</label>
      <br />
      <input type="radio" id="two" value="Two" v-model="picked" />
      <label for="two">Two</label>
      <br />
      <span>Picked: {{ picked }}</span>
    </div>

    <div id="select-example">
      <p :style="{ fontWeight: 'bold' }">{{ "select example" }}</p>
      <select v-model="selected">
        <option value="1">A</option>
        <option value="2">B</option>
        <option value="3">C</option>
      </select>
      <span>Selected: {{ selected }}</span>
    </div>

    <div id="select-multi-example">
      <p :style="{ fontWeight: 'bold' }">{{ "select multi example" }}</p>
      <select v-model="selected2" multiple style="width: 100px">
        <option
          v-for="option in options"
          :value="option.value"
          :key="option.id"
        >
          {{ option.text }}
        </option>
      </select>
      <span>Selected: {{ selected2.join(",") }}</span>
    </div>
  </div>
</template>

<script>
const todoItem = {
  props: ["title"],
  template:
    "<li>{{ title }}<button v-on:click=\"$emit('remove')\">X</button></li>",
};
export default {
  name: "app04",
  data() {
    return {
      newTodoText: "",
      todos: [
        { id: 1, text: "Do the dishes" },
        { id: 2, text: "Take out the trash" },
        { id: 3, text: "Mow the lawn" },
      ],
      checkedNames: [],
      picked: [],
      options: [
        { id: "1", text: "One", value: "A" },
        { id: "2", text: "Two", value: "B" },
        { id: "3", text: "Three", value: "C" },
      ],
      selected: [],
      selected2: [],
    };
  },
  methods: {
    addNewTodo() {
      this.todos.push({ id: 4, text: this.newTodoText });
      this.newTodoText = "";
    },
  },
  components: {
    todoItem,
  },
};
</script>