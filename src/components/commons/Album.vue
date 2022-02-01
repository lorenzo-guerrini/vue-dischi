<template>
  <div class="album">
    <a href="#">
      <div class="cover">
        <img :src="info.poster" alt="" />
      </div>

      <div class="info">
        <div class="title">{{ info.title }}</div>
        <div class="author">{{ info.author }}</div>
        <div class="year">{{ info.year }}</div>
      </div>
    </a>
  </div>
</template>

<script>
export default {
  name: "Album",
  props: {
    info: Object,
  },
};
</script>

<style lang="scss" scoped>
@import "../../assets/style/vars.scss";

.album {
  width: 134px;
  height: 240px;

  margin: 13px;
  padding: 13px;

  display: flex;
  flex-direction: column;
  align-items: center;

  background-color: $primary-color;

  overflow: hidden;

  .cover {
    width: 108px;
    height: 108px;

    overflow: hidden;

    img {
      width: 100%;
    }
  }

  .info {
    margin-top: 13px;

    text-align: center;

    .title {
      font-size: 14px;
      font-weight: bold;
      color: $primary-text-color;

      text-transform: uppercase;

      margin-bottom: 13px;
    }

    .author,
    .year {
      font-weight: normal;

      color: $secondary-text-color;
    }

    .author {
      font-size: 12px;
    }

    .year {
      font-size: 11px;
    }
  }
}
</style>
