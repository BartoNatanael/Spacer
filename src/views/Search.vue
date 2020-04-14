<template>
  <div class="wrapper">
    <Claim/>
    <SearchInput v-model="searchValue" @input="handleInput"/>

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
    margin: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin: 0;
    padding: 30px;
    width: 100%;
    height: 100vh;
    // background-image: url('../images/back.jpg');
    // background-repeat: no-repeat;
    // background-size: cover;
    // background-position: 20% 0%;
    color: white;
  }
</style>
