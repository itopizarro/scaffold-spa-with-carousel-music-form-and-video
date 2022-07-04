<template>
  <section>
    <video controls>
      <source src="foo.webmv" type="video/webm" />
      <source src="foo.mp4" type="video/mp4" />
      Sorry, your browser doesn't support embedded videos.
    </video>
    <h2>Lorem ipsum dolor sit amet consectetur.</h2>
    <form>[form]</form>
  </section>
</template>
<script>
// setup Vueify
export default {
  name: "FrameThree",
  data() {
    return {
      inputEmail: "",
      inputConfirmEmail: "",
      inputUsername: "",
      showConfirmation: false,
    };
  },
  methods: {
    submitForm(event) {
      // AJAX
    },
    onAJAXResponse() {
      // respond to response
      // async?
    },
    playVideo() {
      // async?
      this.$emit("pause-music");
      // do playing
      this.videoIsPlaying = true;
    },
    pauseVideo() {
      // async?
      // do pausing
      this.videoIsPlaying = false;
      this.$emit("play-music");
    },
  },
};
</script>