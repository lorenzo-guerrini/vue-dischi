<template>
<div>
    <div v-if="!loading" class="container">
        <Album v-for="(element, i) in albumsArray" :key="i" :info="element" /> 
    </div>
    <div v-else class="loader">
        Loading...
    </div>
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
            albumsArray: [],
            loading: true
        }
    },
    components: {
        Album
    },
    methods: {
        getAlbums() {
            axios.get(this.apiURL).then((apiResponse) => {
                this.albumsArray = apiResponse.data.response;
                this.loading = false;
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

.loader {
    text-align: center;
    color: white;

    padding-top: 50px;
}
</style>