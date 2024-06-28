<template>
  <div class="movie-add-form">
    <h3>Add new movie</h3>
    <form class="add-form d-flex" @submit.prevent>
      <input
        type="text"
        class="form-control new-movie-label"
        placeholder="What movie ?"
        :value="name"
        @input="name = $event.target.value"
      />
      <input
        type="number"
        class="form-control new-movie-label"
        placeholder="Watched count?"
        :value="viewers"
        @input="viewers = $event.target.value"
      />

      <button class="btn btn-outline-success" type="submit" @click="addMovie()">
        Add
      </button>
    </form>
  </div>
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
      if (this.name || !this.viewers) return;
      const newMovie = {
        name: this.name,
        viewers: this.viewers,
        favorite: false,
        like: false,
        id: Date.now(),
      };
      this.$emit("createMovie", newMovie);
      //this.$emit( "funksiya nomi" , function argument)
      //Endi esa inputdagi valuelarni remove qilish uchun name va viewersni empty qilamiz
      (this.name = ""), (this.value = "");
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
