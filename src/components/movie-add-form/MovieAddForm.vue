<template>
  <Box class="movie-add-form">
    <h3>Add new movie</h3>
    <form class="add-form d-flex" @submit.prevent>
      <Input
        class="new-movie-label"
        placeholder="Which movie?"
        v-model="name"
      />

      <Input
        type="number"
        class="new-movie-label"
        placeholder="How many times watched?"
        v-model="viewers"
      />

      <PrimaryButton
        class="btn-outline-success"
        type="submit"
        @click="addMovie()"
      >
        Add
      </PrimaryButton>
    </form>
  </Box>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      viewers: "",
    };
  },
  methods: {
    addMovie() {
      if (!this.name || !this.viewers) return;
      const newMovie = {
        name: this.name,
        viewers: this.viewers,
        favorite: false,
        like: false,
      };
      this.$emit("createMovie", newMovie);
      //this.$emit( "funksiya nomi" , function argument)
      //Endi esa inputdagi valuelarni remove qilish uchun name va viewersni empty qilamiz
      (this.name = ""), (this.viewers = "");
    },
  },
};
</script>

<style>
.movie-add-form {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
