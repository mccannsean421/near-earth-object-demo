<template>
  <div id="app">
    <Map />
  </div>
</template>

<script>
import axios from 'axios';
import moment from 'moment';
import Map from './components/map.vue';

export default {
  name: 'App',
  components: {
    Map,
  },
  async created() {
    const date = new Date();
    const today = moment(date).format('YYYY-MM-DD')
    const key = process.env.VUE_APP_API_KEY;
    const feed = await axios.get(`/neo/rest/v1/feed?start_date=2021-02-19&end_date=${today}&api_key=${key}`);
    console.log(feed.data.near_earth_objects[today]);
  }
}
</script>

<style>
#info {
	position: absolute;
	top: 10px;
	width: 100%;
	text-align: center;
	z-index: 100;
	display:block;
}
</style>
