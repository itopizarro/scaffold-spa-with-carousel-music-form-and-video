<template>
  <section>
    <object>
      <code>[game]</code>
      <button @click.prevent="onClickSolve">Solve the game</button>
    </object>
    <div :class="['forest', { reveal: gameIsSolved }]">
      <div class="message" v-if="gameIsSolved">
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Laudantium
          animi perspiciatis esse! Impedit culpa rerum laborum sunt quos fugiat
          obcaecati.
        </p>
        <button
          @click.prevent="onClickNextFrame"
          :disabled="this.currentFrame !== 1"
        >
          Next
        </button>
      </div>
    </div>
  </section>
</template>
<script>
// has to emit Next click to parent
export default {
  name: "FrameOne",
  data() {
    return {
      gameIsSolved: false,
    };
  },
  props: {
    currentFrame: {
      type: Number,
    },
  },
  methods: {
    onClickSolve(event) {
      this.gameIsSolved = true;
    },
    onClickNextFrame(event) {
      // prevent anachronistic keyboard navigation clicks
      if (this.currentFrame !== 1) {
        return;
      }
      this.$emit("next-frame");
    },
  },
};
</script>