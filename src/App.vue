<template>
  <table>
    <tr>
      <th>musicIsPlaying</th>
      <td v-text="musicIsPlaying"></td>
    </tr>
    <tr>
      <th>currentFrame</th>
      <td v-text="currentFrame"></td>
    </tr>
    <tr>
      <th>controlFrame</th>
      <td v-text="controlFrame"></td>
    </tr>
  </table>
  <FloatingHeader
    :current-frame="currentFrame"
    :is-playing-music="musicIsPlaying"
    :control-frame="controlFrame"
    @toggle-music="onToggleMusic"
    @previous-frame="onPreviousFrame"
  />
  <FrameOne
    :class="{ active: currentFrame === 1 }"
    :current-frame="currentFrame"
    @next-frame="onNextFrame"
  />
  <FrameTwo
    :class="{ active: currentFrame === 2 }"
    v-if="currentFrame != 1"
    :current-frame="currentFrame"
    @next-frame="onNextFrame"
    @set-control="setControl"
  />
  <FrameThree
    :class="{ active: currentFrame === 3 }"
    v-if="currentFrame != 1"
    @play-music="playMusic"
    @pause-music="pauseMusic"
  />
  <FrameFour :class="{ active: currentFrame === 4 }" v-if="currentFrame == 4" />
  <FloatingFooter :current-frame="currentFrame" @next-frame="onNextFrame" />
</template>

<script>
import FloatingHeader from "./components/Header";
import FloatingFooter from "./components/Footer";
import FrameOne from "./components/FrameOne.vue";
import FrameTwo from "./components/FrameTwo.vue";
import FrameThree from "./components/FrameThree.vue";
import FrameFour from "./components/FrameFour.vue";

export default {
  name: "App",
  data() {
    return {
      currentFrame: 1,
      lastFrame: 4,
      musicIsPlaying: true,
      controlFrame: true,
    };
  },
  components: {
    FloatingHeader,
    FloatingFooter,
    FrameOne,
    FrameTwo,
    FrameThree,
    FrameFour,
  },
  methods: {
    onPreviousFrame() {
      this.decrementFrame();
      // determine whether to decrementFrame OR emit previousSlide
    },
    onNextFrame() {
      this.incrementFrame();
    },
    incrementFrame() {
      if (this.currentFrame < this.lastFrame) {
        this.currentFrame += 1;
      }
    },
    decrementFrame() {
      if (this.currentFrame > 1) {
        this.currentFrame -= 1;
      }
    },
    playMusic() {
      // async?
      // do playing
      this.musicIsPlaying = true;
    },
    pauseMusic() {
      // async?
      // do pausing
      this.musicIsPlaying = false;
    },
    onToggleMusic(event) {
      if (this.musicIsPlaying) {
        this.pauseMusic();
      } else {
        this.playMusic();
      }
    },
    setControl(string) {
      this.controlFrame = string === "frame";
    },
  },
};
</script>
<style lang="scss" scoped>
table {
  position: fixed;
  top: 0;
  right: 0;
  z-index: 2;
  background-color: rgba(black, 0.5);
  color: lime;
  font-family: monospace;
  tr,
  td {
    text-align: left;
  }
}
section {
  opacity: 0.3;
  &.active {
    opacity: 1;
  }
}
</style>