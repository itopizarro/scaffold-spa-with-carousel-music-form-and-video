<template>
  <footer>
    <figure @click="onClickSecret" style="order: 1">
      <img src="http://placekitten.com/100" alt="placeholding kitten" />
    </figure>
    <p :style="{ order: currentFrame === 3 ? 3 : 2 }">
      Lorem, ipsum dolor sit amet consectetur adipisicing elit. Ea, vero.
    </p>
    <nav :style="{ order: currentFrame === 3 ? 2 : 3 }">
      <a href="/"><span>Twitter</span></a>
      <a href="/"><span>Twitch</span></a>
      <a href="/"><span>YouTube</span></a>
    </nav>
  </footer>
</template>
<script>
export default {
  name: "FloatingFooter",
  props: {
    currentFrame: {
      type: Number,
    },
  },
  methods: {
    onClickSecret(event) {
      this.$emit("next-frame");
    },
  },
};
</script>
<style lang="scss" scoped>
footer {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: baseline;
}
p {
  margin: 0;
}
figure {
  margin: 0;
  padding: 0;
  width: 50px;
  img {
    display: block;
    width: 100%;
  }
}
</style>