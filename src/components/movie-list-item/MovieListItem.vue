<template>
  <li class="list-group-item d-flex justify-content-between favourite">
    <span class="list-group-item-label">Empire of Usman</span>
    <input class="list-group-item-input" type="number" defaultValue="811" />

    <div class="d-flex justify-content-center align-items-center">
      <button class="btn-cookie btn-sm" type="button">
        <i class="fas fa-cookie"></i>
      </button>

      <button class="btn-trash btn-sm" type="button">
        <i class="fas fa-trash"></i>
      </button>

      <i class="fas fa-star"></i>
    </div>
  </li>
</template>
<script>
export default {};
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

//! 7-dars => Movie item component. style
