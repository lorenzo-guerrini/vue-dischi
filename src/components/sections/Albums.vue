<template>
  <div class="container">
    <Search
      :genres="genresArray"
      :authors="authorsArray"
      @searchTitle="searchTitle"
      @filterGenre="filterGenre"
      @filterArtist="filterArtist"
    />
    <div v-if="!loading" class="albums-container">
      <Album v-for="(element, i) in searchedAlbums" :key="i" :info="element" />
    </div>
    <Loader v-else />
  </div>
</template>

<script>
import Search from "../commons/Search.vue";
import axios from "axios";
import Album from "../commons/Album.vue";
import Loader from "../commons/Loader.vue";

export default {
  name: "Albums",
  data() {
    return {
      apiURL: "https://flynn.boolean.careers/exercises/api/array/music",
      albumsArray: [],
      genresArray: [],
      authorsArray: [],
      inputSearch: "",
      inputGenre: "All",
      inputArtist: "All",
      loading: true,
    };
  },
  components: {
    Search,
    Loader,
    Album,
  },
  methods: {
    getAlbums() {
      axios
        .get(this.apiURL)
        .then((apiResponse) => {
          //Album
          this.albumsArray = apiResponse.data.response;

          //Generi
          this.genresArray.push("All");
          let tempGenresArray = apiResponse.data.response.map((album) => {
            return album.genre;
          });
          Array.prototype.push.apply(this.genresArray, tempGenresArray);

          //Autori
          this.authorsArray.push("All");
          let tempAuthorsArray = apiResponse.data.response.map((album) => {
            return album.author;
          });
          Array.prototype.push.apply(this.authorsArray, tempAuthorsArray);

          //Fine loading
          this.loading = false;
        })
        .catch(function (error) {
          console.log(error);
        });
    },
    searchTitle(input) {
      this.inputSearch = input;
    },
    filterGenre(input) {
      this.inputGenre = input;
    },
    filterArtist(input) {
      this.inputArtist = input;
    },
  },
  created() {
    this.getAlbums();
  },
  computed: {
    searchedAlbums() {
      return this.albumsArray.filter((album) => {
        if (this.inputGenre == "All" && this.inputArtist == "All") {
          return album.title
            .toLowerCase()
            .includes(this.inputSearch.toLowerCase());
        }

        if (this.inputGenre != "All" && this.inputArtist == "All") {
          return (
            album.title
              .toLowerCase()
              .includes(this.inputSearch.toLowerCase()) &&
            album.genre.toLowerCase().includes(this.inputGenre.toLowerCase())
          );
        }

        if (this.inputGenre == "All" && this.inputArtist != "All") {
          return (
            album.title
              .toLowerCase()
              .includes(this.inputSearch.toLowerCase()) &&
            album.author.toLowerCase().includes(this.inputArtist.toLowerCase())
          );
        }

        return (
          album.title.toLowerCase().includes(this.inputSearch.toLowerCase()) &&
          album.genre.toLowerCase().includes(this.inputGenre.toLowerCase()) &&
          album.author.toLowerCase().includes(this.inputArtist.toLowerCase())
        );
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  text-align: center;
  padding-top: 40px;
}

.albums-container {
  width: 900px;

  margin: auto;
  padding: 40px 0;

  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
</style>
