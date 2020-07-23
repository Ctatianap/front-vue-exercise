<template>
  <div
    v-if="win"
    class="shadow-2xl bg-blue-100 border-t border-b border-blue-500 text-blue-700 px-4 py-3 w-3/4 my-5"
    role="alert"
    :style="styleObject"
  >
    <p>
      <i v-if="win === 'X'" class="fas fa-cat text-6xl"></i>
      <i v-if="win === 'O'" class="fas fa-fish text-6xl"></i>
    </p>
    <p class="font-bold text-4xl">
      {{ win === "Empate" ? "Empate u_u" : "¡¡Ganaste!!" }}
    </p>

    <img
      v-if="win === 'X'"
      src="../assets/CatWin.gif"
      alt="cat win"
      class="m-auto my-8"
    />
    <img
      v-if="win === 'O'"
      src="../assets/FishWin.gif"
      alt="fish win"
      class="m-auto my-8"
    />
  </div>
</template>

<script>
export default {
  name: "BannerWin",
  props: {
    win: String,
  },
  data() {
    return {
      styleObject: {
        border: " 3px solid #F2DDD0",
        "background-color": "rgb(255 251 248)",
        color: "#8EB6BF",
      },
    };
  },
};
</script>
