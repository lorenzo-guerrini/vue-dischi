<template>
<div class="container">
    <Album v-for="(element, i) in albumsArray" :key="i" :info="element" /> 
</div>
</template>

<script>
import axios from "axios";
import Album from "../commons/Album.vue"

export default {
    name: "Albums",
    data() {
        return {
            apiURL: "https://flynn.boolean.careers/exercises/api/array/music",
            albumsArray: []
        }
    },
    components: {
        Album
    },
    methods: {
        getAlbums() {
            axios.get(this.apiURL).then((apiResponse) => {
                this.albumsArray = apiResponse.data.response;
            })
            .catch(function (error) {
                console.log(error);
            })
        }
    },
    created() {
        this.getAlbums();
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