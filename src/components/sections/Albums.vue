<template>
  <div class="container">
    <Search
      :genres="genresArray"
      :authors="authorsArray"
      @searchTitle="searchTitle"
      @filterGenre="filterGenre"
      @filterAuthor="filterAuthor"
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
      inputAuthor: "All",
      loading: true,
    };
  },
  components: {
    Search,
    Loader,
    Album,
  },
  methods: {
    //Ottiene dall'API l'array degli album e lo usa per riempire albumsArray, genresArray e authorsArray
    getAlbums() {
      axios
        .get(this.apiURL)
        .then((apiResponse) => {
          //albumsArray
          this.albumsArray = apiResponse.data.response;

          //genresArray
          this.genresArray.push("All");

          apiResponse.data.response.forEach((album) => {
            if (!this.genresArray.includes(album.genre)) {
              this.genresArray.push(album.genre);
            }
          });

          //authorsArray
          this.authorsArray.push("All");

          apiResponse.data.response.forEach((album) => {
            if (!this.authorsArray.includes(album.author)) {
              this.authorsArray.push(album.author);
            }
          });

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
    filterAuthor(input) {
      this.inputAuthor = input;
    },
  },
  created() {
    this.getAlbums();
  },
  computed: {
    searchedAlbums() {
      return this.albumsArray.filter((album) => {
        //Filtri attivi: nessuno
        if (this.inputGenre == "All" && this.inputAuthor == "All") {
          return album.title
            .toLowerCase()
            .includes(this.inputSearch.toLowerCase());
        }

        //Filtri attivi: genere
        if (this.inputGenre != "All" && this.inputAuthor == "All") {
          return (
            album.title
              .toLowerCase()
              .includes(this.inputSearch.toLowerCase()) &&
            album.genre.toLowerCase().includes(this.inputGenre.toLowerCase())
          );
        }

        //Filtri attivi: autore
        if (this.inputGenre == "All" && this.inputAuthor != "All") {
          return (
            album.title
              .toLowerCase()
              .includes(this.inputSearch.toLowerCase()) &&
            album.author.toLowerCase().includes(this.inputAuthor.toLowerCase())
          );
        }

        //Filtri attivi: autore e genere
        return (
          album.title.toLowerCase().includes(this.inputSearch.toLowerCase()) &&
          album.genre.toLowerCase().includes(this.inputGenre.toLowerCase()) &&
          album.author.toLowerCase().includes(this.inputAuthor.toLowerCase())
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
