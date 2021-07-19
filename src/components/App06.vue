<template id="app-6">
  <div id="watch-example">
    <p
      class="header-title"
      :style="{ fontSize: 18 + 'px', fontWeight: 'bold' }"
    >
      App06:Ask a yes/no question:
      <input v-model="question" />
    </p>
    <p>{{ answer }}</p>
    <p>parent counter:{{ count }}</p>
    <button @click="showParentCounter">parentClick</button>
    <child-demo :counter="count" @child-event="showChildCounter"></child-demo>
  </div>
</template>

<script>
import _ from "lodash";
import axios from "axios";
import childDemo from "./children/child01";
export default {
  name: "app06",
  data() {
    return {
      question: "",
      answer: "I cannot give you an answer until you ask a question!",
      count: 0,
    };
  },
  watch: {
    // 如果 `question` 发生改变，这个函数就会运行
    question(newQuestion, oldQuestion) {
      this.answer =
        "Waiting for you to stop typing...{" +
        oldQuestion +
        "}:{" +
        newQuestion +
        "}";
      this.debouncedGetAnswer();
    },
  },
  created() {
    // `_.debounce` 是一个通过 Lodash 限制操作频率的函数。
    // 在这个例子中，我们希望限制访问 yesno.wtf/api 的频率
    // AJAX 请求直到用户输入完毕才会发出。想要了解更多关于
    // `_.debounce` 函数 (及其近亲 `_.throttle`) 的知识，
    // 请参考：https://lodash.com/docs#debounce
    this.debouncedGetAnswer = _.debounce(this.getAnswer, 500);
  },
  methods: {
    getAnswer() {
      if (this.question.indexOf("?") === -1) {
        this.answer = "Questions usually contain a question mark. ;-)";
        return;
      }
      this.answer = "Thinking...";
      var vm = this;
      axios
        .get("https://yesno.wtf/api")
        .then(function (response) {
          vm.answer = _.capitalize(response.data.answer);
        })
        .catch(function (error) {
          vm.answer = "Error! Could not reach the API. " + error;
        });
    },
    showParentCounter() {
      this.count++;
    },
    showChildCounter(childCounter) {
      this.count = childCounter + 2;
    },
  },
  components: {
    childDemo,
  },
};
</script>