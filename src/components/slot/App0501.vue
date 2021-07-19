<template id="child-slot-example">
  <!-- only one root node -->
  <div>
    <h2>I'm the child title</h2>
    <slot name="slot-01"> if no content then show this message. </slot>
    <slot> no matched show here! </slot>
  </div>
</template>

<script>
export default {
  name: "my-slot-component",
};
</script>