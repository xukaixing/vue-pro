<template id="app-6">
  <div id="watch-example">
    <p class="header-title" :style="{ fontSize: 18 + 'px', fontWeight: 'bold' }">
      App06:Ask a yes/no question:
      <input v-model="question" />
    </p>
    <p>{{ answer }}</p>
    <p>parent counter:{{ count }}</p>
    <button @click="showParentCounter">parentClick</button>
    <child-demo :counter="count" :username-change.sync="username" @child-event="showChildCounter"></child-demo>
    <p>show child componets:</p>
    <base-input label="Username:" v-model="username" @blur="doBlur" required placeholder="Enter your username"></base-input>
    <p>show child checkbox:</p>
    <base-checkbox v-model="isChecked" :value="username"></base-checkbox>
  </div>
</template>

<script>
import _ from 'lodash';
import axios from 'axios';
import childDemo from './children/child01';
import baseInput from './base/base-input';
import baseCheckbox from './base/base-checkbox';
export default {
  name: 'app06',
  data() {
    return {
      question: '',
      answer: 'I cannot give you an answer until you ask a question!',
      count: 0,
      username: 'andyten',
      isChecked: true,
    };
  },
  watch: {
    // 如果 `question` 发生改变，这个函数就会运行
    question(newQuestion, oldQuestion) {
      this.answer = 'Waiting for you to stop typing...{' + oldQuestion + '}:{' + newQuestion + '}';
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
      if (this.question.indexOf('?') === -1) {
        this.answer = 'Questions usually contain a question mark. ;-)';
        return;
      }
      this.answer = 'Thinking...';
      var vm = this;
      axios
        .get('https://yesno.wtf/api')
        .then(function(response) {
          vm.answer = _.capitalize(response.data.answer);
        })
        .catch(function(error) {
          vm.answer = 'Error! Could not reach the API. ' + error;
        });
    },
    /**
     * 显示父级counter
     */
    showParentCounter() {
      this.count++;
    },
    /**
     * 显示子组件counter，主要为实现子组件出发更新父组件属性
     * 更新父组件属性，自动影响子组件属性
     */
    showChildCounter(childCounter) {
      this.count = childCounter + 2;
    },
    doBlur() {
      alert(this.count);
    },
  },
  components: {
    childDemo,
    baseInput,
    baseCheckbox,
  },
};
</script>
