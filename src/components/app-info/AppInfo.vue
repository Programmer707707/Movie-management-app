<template>
  <Box class="box">
    <p class="fs-3 text">All Movies: {{ allMoviesCount }}</p>
    <p class="fs-4 text">Favorite movies: {{ favouriteCount }}</p>
  </Box>
</template>

<script>
export default {
  props: {
    allMoviesCount: {
      type: Number,
      required: true,
    },
    favouriteCount: {
      type: Number,
      required: true,
    },
  },
};
</script>

<style scoped>
.box {
  /* From https://css.glass */
  backdrop-filter: blur(16px) saturate(180%);
  -webkit-backdrop-filter: blur(16px) saturate(180%);
  background-color: #fcfaf5;
  border-radius: 12px;
  border: 2px solid rgba(73, 73, 74, 0.3);
}
</style>
