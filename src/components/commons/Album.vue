<template>
  <div class="album">
      <div class="cover">
          <img src="https://www.onstageweb.com/wp-content/uploads/2018/09/bon-jovi-new-jersey.jpg" alt="">
      </div>

      <div class="info">
          <div class="title">New Jersey</div>
          <div class="author">Bon Jovi</div>
          <div class="year">1988</div>
      </div>
  </div>
</template>

<script>
export default {
    name: "Album"
}
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
            font-size: 15px;
            font-weight: bold;
            color: $primary-text-color;

            text-transform: uppercase;

            margin-bottom: 13px;
        }

        .author, .year {
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