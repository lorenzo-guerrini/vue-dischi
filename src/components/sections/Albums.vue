<template>
<div class="container">
    <Album v-for="(element, i) in 10" :key="i" /> 
</div>
</template>

<script>
import Album from "../commons/Album.vue"

export default {
    name: "Albums",
    components: {
        Album
    }
}
</script>

<style lang="scss" scoped>
.container {
    width: 900px;

    margin: auto;
    padding: 40px 0;

    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}
</style>