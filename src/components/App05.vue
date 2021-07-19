<template id="app-5">
  <div id="app-5">
    <div id="parent-slot-example">
      <p
        class="header-title"
        :style="{ fontSize: 18 + 'px', fontWeight: 'bold' }"
      >
        App05:Component Slot
      </p>
      <h1>I'm the parent title</h1>
      <my-slot-component>
        <p slot="slot-01">This is some original content</p>
        <p>This is some more original content</p>
      </my-slot-component>
    </div>
  </div>
</template>

<script>
import mySlotComponent from "@/components/slot/App0501";
export default {
  name: "app05",
  data() {
    return {};
  },
  components: {
    mySlotComponent,
  },
};
</script>