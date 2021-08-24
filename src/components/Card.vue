"<template>
  <div class="card">
    <div class="card-side front" v-if="visible">Front</div>
    <div class="card-side back" v-else>Back</div>
  </div>
</template>

<script>
export default {
  props: {
    visible: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style>
.card {
  width: 100%;
  height: 100%;
  border: 1px solid #000;
  position: relative;
}
.card-side {
  position: absolute;
  width: 100%;
  height: 100%;
}
.card-side.back {
  background-color: rgb(74, 230, 74);
}
.card-side.front {
  background-color: rgb(0, 187, 255);
}
</style>