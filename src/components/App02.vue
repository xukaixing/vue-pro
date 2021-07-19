<template id="app-2">
  <div id="app-2">
    <p
      class="header-title"
      :style="{ fontSize: 18 + 'px', fontWeight: 'bold' }"
    >
      {{ "App02" + ":" + message }}
    </p>
    <button @click="reverseMessage($event)">Reverse Message</button>
  </div>
</template>

<script>
export default {
  name: "app02",
  data() {
    return {
      message: "Hello Bind Method!",
    };
  },
  methods: {
    reverseMessage(event) {
      alert(event.target.tagName);
      // 原生event
      event.preventDefault();
      this.message = this.message.split("").reverse().join("");
    },
  },
};
</script>