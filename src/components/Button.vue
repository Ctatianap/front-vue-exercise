<template>
  <button
    @click="onClick()"
    class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full m-6 my-8"
    :style="{ 'background-color': '#8EB6BF' }"
  >
    <slot />
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    onClick: Function,
    value: String,
  },
};
</script>
