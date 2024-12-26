<template>
  <Box class="movie-add-form">
    <h3>Yangi kino qo'shish</h3>
    <form class="add-form d-flex" @submit.prevent>
      <Input
        class="new-movie-label"
        v-model="title"
        placeholder="Qanday kino?"
      />
      <Input
        class="new-movie-label"
        type="number"
        v-model="viewers"
        placeholder="Qancha marotaba ko'rilgan?"
      />
      <PrimaryButton class="btn-outline-dark" @click="addMovie" type="submit">
        Qo'shish
      </PrimaryButton>
    </form>
  </Box>
</template>
<script>
export default {
  data() {
    return {
      title: "",
      viewers: "",
    };
  },
  methods: {
    addMovie() {
      if (!this.title || !this.viewers) return;
      const newMovie = {
        title: this.title,
        viewers: this.viewers,
        favorite: false,
        like: false,
        id: Date.now(),
      };
      this.$emit("createMovie", newMovie);
      this.title = "";
      this.viewers = "";
    },
  },
  unmounted() {
    console.log("Unmounted");
  },
};
</script>
<style scoped>
.movie-add-form {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
