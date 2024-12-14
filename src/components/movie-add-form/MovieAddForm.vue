<template>
  <div class="movie-add-form">
    <h3>Yangi kino qo'shish</h3>
    <form class="add-form d-flex" @submit.prevent>
      <input
        class="form-control new-movie-label"
        @input="title = $event.target.value"
        type="text"
        placeholder="Qanday kino?"
        :value="title"
      />
      <input
        class="form-control new-movie-label"
        @input="viewers = $event.target.value"
        type="text"
        placeholder="Qancha marotaba ko'rilgan?"
        :value="viewers"
      />
      <button class="btn btn-outline-dark" @click="addMovie" type="submit">
        Qo'shish
      </button>
    </form>
  </div>
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
