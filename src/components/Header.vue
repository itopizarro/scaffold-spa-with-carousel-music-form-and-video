<template>
  <header>
    <button
      @click.prevent="onClickToggleMusic"
      :class="{ playing: isPlayingMusic, paused: !isPlayingMusic }"
    >
      {{ isPlayingMusic ? "Pause" : "Play" }} Music
    </button>
    <button @click.prevent="onClickUpArrow" v-if="currentFrame != 1">
      Previous {{ useFrameControl ? "Frame" : "Slide" }}
    </button>
  </header>
</template>
<script>
import EventBus from "../eventBus.js";
export default {
  name: "FloatingHeader",
  props: {
    currentFrame: {
      type: Number,
    },
    isPlayingMusic: {
      type: Boolean,
    },
    controlFrame: {
      type: Boolean,
      default() {
        return true;
      },
    },
  },
  computed: {
    useFrameControl() {
      return this.currentFrame !== 2 || this.controlFrame;
    },
  },
  methods: {
    onClickToggleMusic(event) {
      this.$emit("toggle-music");
    },
    onClickUpArrow(event) {
      if (this.useFrameControl) {
        this.$emit("previous-frame");
      } else {
        EventBus.$emit("previous-slide");
      }
    },
  },
  // mounted() {
  //   EventBus.$on();
  // }
};
</script>