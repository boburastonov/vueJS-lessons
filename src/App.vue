<template>
  <div class="container">
    <h1>Counter: {{ counter }}</h1>
    <div class="d-flex">
      <button @click="onDecrement" class="btn btn-danger">Delete</button>
      <button @click="onReset" class="btn btn-danger">Reset</button>
      <button @click="onIncrement" class="btn btn-success">Add</button>
    </div>

    <h2 v-if="isAgeVisible">My age is: {{ age }}</h2>
    <h2 v-show="isAgeVisible">Hello EveryBody</h2>
    <button @click="showOrHideAge">
      <span v-if="!isAgeVisible">Show Age</span>
      <span v-if="isAgeVisible">Hide Age</span>
    </button>
    <br />

    <div class="box" @mouseover="handleEvent">mouseover</div>
    <div class="box" @mouseleave="handleEvent">mouseleave</div>
    <div class="box" @dblclick="handleEvent">doubleclick</div>
    <div class="box" @mousemove="handlePosition">
      mousemove <br />
      Position {{ x }}:{{ y }}
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      counter: 10,
      age: 19,
      isAgeVisible: true,
      x: 0,
      y: 0,
    };
  },
  methods: {
    onIncrement() {
      this.counter += 1;
    },
    onDecrement() {
      this.counter -= 1;
    },
    onReset() {
      this.counter = 0;
    },
    showOrHideAge() {
      this.isAgeVisible = !this.isAgeVisible;
    },
    handleEvent(event) {
      console.log("event: " + event.type);
    },
    handlePosition(event) {
      this.x = event.offsetX;
      this.y = event.offsetY;
    },
  },
};
</script>
<style lang=""></style>
0ol,
