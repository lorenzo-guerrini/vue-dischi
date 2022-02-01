<template>
<main>
    <Albums />
</main>
</template>

<script>
import Albums from "../sections/Albums.vue"
export default {
    name: "Main",
    components: {
        Albums
    }
}
</script>

<style lang="scss" scoped>
@import "../../assets/style/vars.scss";

main {
    min-height: calc(100vh - 48px);
    background-color: $bg-color;
}
</style>