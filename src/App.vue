<template>
  <div>
    <img class="logo" src="./assets/logo.svg"/>
    <input class="input" @input="updateFilter($event.target.value)">
    <PhotoList :photos="getPhotos"/>
  </div>
</template>

<script>

import PhotoList from "@/components/PhotoList.vue";
import debounce from "lodash.debounce";

export default {
  name: 'App',
  components: {PhotoList},
  data() {
    return {
      photos: [],
      albums: [],
      filter: null,
    };
  },
  mounted() {
    this.fetchAlbums().then(this.fetchPhotos);

  },
  methods: {
    fetchAlbums() {
      return this.fetch('https://jsonplaceholder.typicode.com/albums', this.prepareAlbums);
    },
    fetchPhotos() {
      return this.fetch('https://jsonplaceholder.typicode.com/photos', this.preparePhotos)
    },
    fetch(url, callback) {
      return fetch(url)
          .then((res) => res.json())
          .then(callback)
          .catch(error => {
            console.log(error);
          })
    },
    preparePhotos(photos) {
      this.photos = photos.map(photo => ({
        albumTitle: this.albums[photo.albumId].title,
        ...photo
      }))
    },
    prepareAlbums(albums) {
      albums.forEach(album => {
        this.albums[album.id] = album;
      })
    },
    updateFilter: debounce(function (value) {
      this.filter = value
    }, 3),
  },
  computed: {
    getPhotos() {
      let filter = this.filter;
      if (!filter) {
        return this.photos;
      }
      filter = parseInt(filter);
      if (filter > 0) {
        return this.photos.filter(photo => photo.id === filter)
      } else {
        return this.photos.filter(photo => photo.title.indexOf(this.filter) >= 0)
      }
    }
  }
};
</script>

<style lang="scss">
.logo {
  width: 100px;
  height: 80px;
}

.input {
  height: 20px;
  width: 250px;
  padding: 15px;
  display: block;
  border-color: red !important;
}
</style>
