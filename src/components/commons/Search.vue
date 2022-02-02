<template>
  <div class="container">
      <div>
          <input type="text" v-model="inputText" placeholder="Cerca per titolo" @keyup="$emit('searchTitle', inputText)">
          <button @click="$emit('search', inputText)">Cerca</button>
      </div>
      <div>
          <span>Filter by genre: </span>
          <select v-model="inputGenre" @change="$emit('filterGenre', inputGenre)">
            <option v-for="(genre, i) in genres" :key="i">{{genre}}</option>
         </select>
      </div>
      <div>
          <span>Filter by artist: </span>
          <select v-model="inputArtist" @change="$emit('filterArtist', inputArtist)">
              <option v-for="(artist, i) in artists" :key="i">{{artist}}</option>
         </select>
      </div>
  </div>
</template>

<script>
export default {
name: "Search",
    data() {
        return {
            genres: [
                "all",
                "rock",
                "pop",
                "jazz",
                "metal"
            ],
            artists: [
                "all",
                "bon jovi",
                "queen",
                "sting",
                "steve gaddband",
                "iron maiden",
                "eric clapton",
                "deep purple",
                "metallica",
                "david wecki",
                "michael jacjson",
            ],
            inputText: "",
            inputGenre: "all",
            inputArtist: "all",
        }
    }
}
</script>

<style lang="scss" scoped>
.container {
    color: white;
}
</style>