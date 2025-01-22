<template>
  <nav aria-label="pagination">
    <ul class="pagination">
      <!-- Previous button -->
      <li class="page-item">
        <a
          class="page-link"
          href="#"
          aria-label="Previous"
          @click.prevent="changePage(page - 1)"
          :disabled="page === 1"
        >
          <span aria-hidden="true">&laquo;</span>
        </a>
      </li>

      <!-- Page number buttons -->
      <li
        class="page-item"
        v-for="pageNumber in totalPages"
        :key="pageNumber"
        :class="{ active: pageNumber === page }"
      >
        <a class="page-link" href="#" @click.prevent="changePage(pageNumber)">
          {{ pageNumber }}
        </a>
      </li>

      <!-- Next button -->
      <li class="page-item">
        <a
          class="page-link"
          href="#"
          aria-label="Next"
          @click.prevent="changePage(page + 1)"
          :disabled="page === totalPages"
        >
          <span aria-hidden="true">&raquo;</span>
        </a>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  props: {
    totalPages: {
      type: Number,
      required: true,
    },
    page: {
      type: Number,
      required: true,
    },
  },
  methods: {
    changePage(newPage) {
      if (newPage > 0 && newPage <= this.totalPages) {
        this.$emit("update:page", newPage); // Emit the new page number
      }
    },
  },
};
</script>

<style scoped>
.pagination .page-item.active .page-link {
  background-color: #007bff;
  border-color: #007bff;
  color: white;
}
</style>
