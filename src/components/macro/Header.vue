<template>
  <header>
    <div class="logo">
      <a href="#">
        <img
          src="https://upload.wikimedia.org/wikipedia/commons/1/19/Spotify_logo_without_text.svg"
          alt="Spotify"
        />
      </a>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style lang="scss" scoped>
@import "../../assets/style/vars.scss";

header {
  background-color: $primary-color;
  height: 48px;

  display: flex;
  align-items: center;
}

.logo {
  height: 32px;
  margin-left: 15px;

  img {
    height: 100%;
  }
}
</style>
