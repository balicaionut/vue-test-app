<script>
export default {
  props: {
    position: {
      type: Number,
      required: true,
    },
    value: {
      type: String,
      required: true,
    },
    visible: {
      type: Boolean,
      default: false,
    },
  },
  setup(props, context) {
    const selectCard = () => {
      context.emit("select-card", {
        position: props.position,
        faceValue: props.value,
      });
    };

    return {
      selectCard,
    };
  },
};
</script>

<template>
  <div class="card" @click="selectCard">
    <div v-if="visible" class="card-face is-front">
      {{ value }}
    </div>
    <div v-else class="card-face is-back">?</div>
  </div>
</template>

<style>
.card {
  border: 5px solid #ccc;
  position: relative;
}
.card-face {
  width: 100%;
  height: 100%;
  position: absolute;
}

.card-face.is-front {
  background-color: rgb(225, 250, 250);
  color: black;
  font-size: 80px;
  text-align: center;
}

.card-face.is-back {
  background-color: rgb(200, 250, 250);
  color: black;
  font-size: 80px;
  text-align: center;
}
</style>
