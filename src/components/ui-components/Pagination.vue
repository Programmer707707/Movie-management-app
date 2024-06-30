<template>
  <nav aria-label="pagination">
    <ul class="pagination pagination-sm">
      <li
        v-for="pageNumber in totalPage"
        :key="pageNumber"
        :pageNumber="pageNumber"
        :class="{ active: pageNumber === page }"
        @click="$emit('onChangePageHandler', pageNumber)"
      >
        <span class="page-link">{{ pageNumber }}</span>
      </li>
    </ul>
  </nav>
</template>
<script>
export default {
  name: "Pagination",
  props: {
    totalPage: {
      type: Number,
      required: true,
    },
    page: {
      type: Number,
      required: true,
    },
  },
};
</script>
<style></style>
