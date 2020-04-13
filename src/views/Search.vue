<template>
  <div class="wrapper">
    <Claim/>
    <SearchInput/>

    <!-- <ul>
      <li v-for='item in result' :key='item.data[0].nasa_id'>
        <p>{{ item.data[0].description }}</p>
      </li>
    </ul> -->
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/searchInput.vue';
// eslint-disable-next-line import/no-unresolved, import/no-extraneous-dependencies

const API = 'https://images-api.nasa.gov';
export default {
  name: 'Search',
  components: { Claim, SearchInput },
  data() {
    return {
      searchValue: '',
      result: [],
    };
  },
  methods: {
    handleInput: debounce(function () {
      axios.get(`${API}/search?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.result = response.data.collection.items;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang="scss" scoped>
  .wrapper{
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0;
    padding: 30px;
    width: 100%;
  }
</style>
