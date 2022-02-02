<template>
  <div class="container">
    <div>
      <input
        type="text"
        id="search-bar"
        v-model="inputText"
        placeholder="Cerca per titolo"
        @keyup="$emit('searchTitle', inputText)"
      />
      <button @click="$emit('search', inputText)">Cerca</button>
    </div>
    <div class="filter">
      <span>Filter by genre: </span>
      <select v-model="inputGenre" @change="$emit('filterGenre', inputGenre)">
        <option v-for="(genre, i) in genres" :key="i">{{ genre }}</option>
      </select>
    </div>
    <div class="filter">
      <span>Filter by artist: </span>
      <select
        v-model="inputArtist"
        @change="$emit('filterArtist', inputArtist)"
      >
        <option v-for="(artist, i) in artists" :key="i">{{ artist }}</option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      genres: ["All", "Rock", "Pop", "Jazz", "Metal"],
      artists: [
        "All",
        "Bon Jovi",
        "Queen",
        "Sting",
        "Steve Gadd Band",
        "Iron Maiden",
        "Eric Clapton",
        "Deep Purple",
        "Metallica",
        "Dave Weckl",
        "Michael Jacjson",
      ],
      inputText: "",
      inputGenre: "All",
      inputArtist: "All",
    };
  },
};
</script>

<style lang="scss" scoped>
@import "../../assets/style/vars.scss";

.container {
  color: white;

  font-size: 14px;
}

#search-bar {
  width: 500px;
  padding: 8px 12px;

  border: 5px solid $primary-color;
  border-radius: 50px;

  background: none;
  color: $primary-text-color;

  &:focus {
    outline: none;
  }
}

button {
  margin: 0 10px;
  padding: 13px 17px;

  border: 0;
  border-radius: 50px;

  background: $primary-color;
  color: $primary-text-color;

  cursor: pointer;
}

.filter {
  margin: 10px 10px;
  display: inline-block;

  select {
    color: white;
    background-color: $bg-color;

    border: 3px solid $primary-color;
    border-radius: 50px;

    margin: 0 5px;
    padding: 3.5px 6px;

    cursor: pointer;

    &:focus {
      outline: none;
    }
  }
}
</style>
