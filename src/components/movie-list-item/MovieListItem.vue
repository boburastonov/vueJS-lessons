<template>
  <li
    class="list-group-item d-flex justify-content-between"
    :class="[{ like: movi.like }, { favourite: movi.favourite }]"
  >
    <span
      class="list-group-item-label"
      @click="$emit('onToggle', { id: movi.id, prop: 'like' })"
      >{{ movi.title }}</span
    >
    <input class="list-group-item-input" type="number" :value="movi.viewers" />

    <div class="d-flex justify-content-center align-items-center">
      <button
        class="btn-cookie btn-sm"
        @click="$emit('onToggle', { id: movi.id, prop: 'favourite' })"
        type="button"
      >
        <i class="fas fa-cookie"></i>
      </button>

      <button
        class="btn-trash btn-sm"
        @click="$emit('onDelete', movi.id)"
        moe
        type="button"
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
    movi: {
      type: Object,
      required: true,
    },
  },
  methods: {
    handleLike() {
      this.$emit("handleLike", this.movi.id);
    },
    handleFavourite() {
      this.$emit("handleFavourite", this.movi.id);
    },
  },
};
</script>
<style scoped>
.list-group-item {
  padding: 15px 25px;
  border: none;
  border-bottom: 1px solid #3d5a80;
}

.list-group-item:last-child {
  border-bottom: none;
}

.list-group-item span {
  width: 550px;
  line-height: 35px;
  font-size: 20px;
  cursor: pointer;
}

.list-group-item input {
  line-height: 35px;
  font-size: 20px;
  text-align: center;
  border: 0;
  outline: none;
  cursor: pointer;
}

.list-group-item button {
  width: 35px;
  height: 35px;
  margin: 3px;
  font-size: 17px;
  border: none;
  cursor: pointer;
}

.list-group-item .btn-cookie {
  color: #ffc107;
}

.list-group-item .btn-trash {
  color: #e74c3c;
}

.list-group-item .fa-star {
  width: 35px;
  height: 35px;
  text-align: center;
  line-height: 35px;
  font-size: 16px;
  color: #ffd700;
  transition: all 0.3s;
  transform: translateX(30px);
  opacity: 0;
}

.list-group-item.like .fa-star {
  opacity: 1;
  transform: translateX(0);
}

.list-group-item.favourite .list-group-item-label,
.list-group-item.favourite .list-group-item-input {
  color: #ffc107;
}
</style>
