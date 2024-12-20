<template>
  <div class="btn-group">
    <PrimaryButton
      v-for="btn in filterButtons"
      :key="btn.value"
      @click="filterHandler(btn.value)"
      :class="[filterName === btn.value ? 'btn-dark' : 'btn-outline-dark']"
      type="button"
    >
      {{ btn.label }}
    </PrimaryButton>
  </div>
</template>
<script>
export default {
  props: {
    onUpdateFilterHandler: {
      type: Function,
      required: true,
    },
    filterName: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      filterButtons: [
        { label: "Barcha kinolar", value: "all" },
        { label: "Mashhur kinolar", value: "popular" },
        { label: "Eng ko'p ko'rilgan kinolar", value: "mostViewers" },
      ],
      filter: "all",
    };
  },
  methods: {
    filterHandler(filter) {
      this.filter = filter;
      this.onUpdateFilterHandler(filter);
    },
  },
};
</script>
<style></style>
