<template>
  <section>
    <object>
      <code>[carousel:slide{{ currentSlide }} of {{ lastSlide }}]</code>
    </object>
    <div class="control">
      <button @click.prevent="onClickNext" :disabled="this.currentFrame !== 2">
        Next {{ currentSlide < lastSlide ? "Slide" : "Frame" }}
      </button>
    </div>
  </section>
</template>
<script>
import EventBus from "../eventBus.js";

// has to emit Next click to parent
export default {
  name: "FrameTwo",
  data() {
    return {
      currentSlide: 1,
      lastSlide: 3,
    };
  },
  props: {
    currentFrame: {
      type: Number,
    },
  },
  methods: {
    goToNextFrame() {
      this.$emit("next-frame");
    },
    nextSlide() {
      // use carousel API
      if (this.currentSlide < this.lastSlide) {
        this.currentSlide += 1;
      }
    },
    previousSlide() {
      // use carousel API
      if (this.currentSlide > 1) {
        this.currentSlide -= 1;
      }
    },
    onClickNext(event) {
      // prevent anachronistic keyboard navigation clicks
      if (this.currentFrame !== 2) {
        return;
      }

      if (this.currentSlide < this.lastSlide) {
        this.nextSlide();
      } else {
        this.goToNextFrame();
      }
    },
  },
  watch: {
    currentSlide(newValue, oldValue) {
      if (newValue === 1) {
        this.$emit("set-control", "frame");
      } else if (oldValue !== newValue) {
        this.$emit("set-control", "slide");
      }
    },
  },
  mounted() {
    // load carousel
    EventBus.$on("previous-slide", this.previousSlide);
  },
};
</script>