<template>
  <div id="app">
    <button @click="fetchNewCat">New Cat</button> <img :src="catImage" alt="Cat Image" />
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  data() {
    return {
      // Were storing the cat image url in this prop
      catImage: null
    };
  },
  created() {
    this.fetchNewCat();
  },
  methods: {
		fetchNewCat() {
			axios
				.get('https://api.thecatapi.com/v1/images/search')
				.then(response => {
					console.log('Search complete!');
					console.log(response);
          this.catImage = response.data[0].url;
				})
				.catch(err => {
					console.log('Search failed!');
					console.log(err);
				});
		},
	},
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
