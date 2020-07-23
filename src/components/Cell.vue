<template>
  <div
    @click="play()"
    class="border-none w-full h-24 sm:h-32 lg:h-48 flex items-center justify-center text-4xl hover:bg-gray-100 cursor-pointer"
    :style="styleObject"
  >
    <i
      v-if="value === 'X'"
      class="fas fa-cat"
      :style="{ color: '#8EB6BF' }"
    ></i>
    <i
      v-if="value === 'O'"
      class="fas fa-fish"
      :style="{ color: '#464659' }"
    ></i>
  </div>
</template>

<script>
export default {
  name: "Cell",
  props: {
    value: String,
    play: Function,
    index: String,
  },
  data() {
    return {
      styleObject: {},
    };
  },
  created() {
    if (
      this.index === "1" ||
      this.index === "2" ||
      this.index === "4" ||
      this.index === "5"
    ) {
      this.styleObject = {
        "border-right": "solid 5px #F2DDD0",
        "border-bottom": "solid 5px #F2DDD0",
      };
    }
    if (this.index === "3" || this.index === "6") {
      this.styleObject = {
        "border-bottom": "solid 5px #F2DDD0",
      };
    }
    if (this.index === "7" || this.index === "8") {
      this.styleObject = {
        "border-right": "solid 5px #F2DDD0",
      };
    }
  },
};
</script>
