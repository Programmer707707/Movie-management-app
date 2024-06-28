<template>
  <li
    class="list-group-item d-flex justify-content-between"
    :class="[{ favorite: movie.favorite }, { like: movie.like }]"
  >
    <span
      @click="$emit('onToggle', { id: movie.id, prop: 'favorite' })"
      class="list-group-item-label"
      >{{ movie.name }}</span
    >
    <input type="number" class="list-group-item-input" :value="movie.viewers" />
    <div class="d-flex justify-content-center align-items-center">
      <button
        type="button"
        class="btn-heart btn-sm"
        @click="$emit('onToggle', { id: movie.id, prop: 'like' })"
      >
        <i class="fas fa-heart"></i>
      </button>

      <button
        type="button"
        class="btn-trash btn-sm"
        @click="$emit('onDelete', movie.id)"
      >
        <i class="fas fa-trash"></i>
      </button>

      <i class="fas fa-star"></i>
    </div>
  </li>
</template>

<script>
export default {
  props: {
    movie: {
      type: Object,
      required: true,
    },
  },
  methods: {},
};
</script>

<style>
.list-group-item {
  padding: 15px 20px;
  border-bottom: 1px solid #3d5a80;
  border: none;
}

.list-group-item:last-child {
  border-bottom: none;
}

.list-group-item span {
  line-height: 35px;
  font-size: 20px;
  cursor: pointer;
  width: 550px;
}

.list-group-item input {
  line-height: 35px;
  font-size: 20px;
  text-align: center;
  border: 0;
}

.list-group-item button {
  width: 35px;
  height: 35px;
  margin: 3px;
  font-size: 17px;
  border: none;
  cursor: pointer;
}

.list-group-item .btn-heart {
  color: #050505;
}

.list-group-item .btn-trash {
  color: #e09f3e;
}

.list-group-item .fa-star {
  width: 35px;
  height: 35px;
  text-align: center;
  line-height: 35px;
  font-size: 16px;
  color: #ffd700;
  transition: 0.3s all;
  transform: translateX(30px);
  opacity: 0;
}

.list-group-item.favorite .fa-star {
  opacity: 1;
  transform: translateX(0);
}

.list-group-item.like .fa-heart {
  color: #ff4646;
}
</style>
