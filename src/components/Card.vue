"<template>
  <div class="card" @click="selectCard">
    <div class="card-side front" v-if="visible">{{ value }}</div>
    <div class="card-side back" v-else>Back</div>
  </div>
</template>

<script>
export default {
  props: {
    position: {
      type: Number,
      required: true,
    },
    value: {
      type: Number,
      required: true,
    },
    visible: {
      type: Boolean,
      default: true,
    },
  },
  setup(props, context) {
    const selectCard = () => {
      context.emit("select-card", {
        position: props.position,
      });
    };

    return {
      selectCard,
    };
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