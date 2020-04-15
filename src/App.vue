<template>
  <div class="app">
    <div :class="[{flexStart: step === 1}, 'wrapper']">
      <transition name='slide'>
        <h3 v-if="step === 1">SPACER</h3>
      </transition>
      <transition name='fade'>
        <heroImage v-if="step === 0"/>
      </transition>
      <Claim v-if="step === 0"/>
      <SearchInput
      v-model="searchValue"
      @input="handleInput"
      :dark='step === 1'
      />
    <div class="results" v-if="result && !loading && step === 1">
      <Item
      v-for="item in result"
      :item="item"
      :key="item.data[0].nasa_id"
      @click.native="handleModalOpen(item)"/>
    </div>
  </div>
  <div class="loader" v-if="step === 1 && loading" />
  <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false"/>
  </div>
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Montserrat:400,600,700,800,900&display=swap');
  *{
    box-sizing: border-box;
  }

  body {
    font-family: 'Montserrat', Arial, sans-serif;
    margin: 0;
    padding: 0;
    color: black;
  }

  h3{
    color: black;
  }

  .results{
    color: black;
  }

  .fade-enter-active, .fade-leave-active {
  transition: opacity .5s ease;
}
  .fade-enter, .fade-leave-to{
   opacity: 0;
  }

  .slide-enter-active, .slide-leave-active {
  transition: margin-top .5s ease;
}
  .slide-enter, .slide-leave-to{
   margin-top: -50px;
  }

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

    &.flexStart{
      justify-content: flex-start;
    }
  }

  .results{
    margin-top: 50px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
    @media(min-width: 768px){
      grid-template-columns: 1fr 1fr 1fr;
    }
  }
  .loader {
  margin-top: 100px;
  display: inline-block;
  width: 64px;
  height: 64px;
  @media (min-width: 768px) {
    width: 90px;
    height: 90px;
  }
}
.loader:after {
  content: " ";
  display: block;
  width: 46px;
  height: 46px;
  margin: 1px;
  border-radius: 50%;
  border: 5px solid #1e3d4a;
  border-color: #1e3d4a transparent #1e3d4a transparent;
  animation: loading 1.2s linear infinite;
  @media (min-width: 768px) {
    width: 90px;
    height: 90px;
  }
}
@keyframes loading {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

</style>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/searchInput.vue';
import HeroImage from '@/components/heroImage.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';
// eslint-disable-next-line import/no-unresolved, import/no-extraneous-dependencies

const API = 'https://images-api.nasa.gov';
export default {
  name: 'Search',
  components: {
    Claim, SearchInput, HeroImage, Item, Modal,
  },
  data() {
    return {
      loading: 'false',
      step: 0,
      searchValue: '',
      result: [],
      modalOpen: false,
      modalItem: null,
    };
  },
  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
    handleInput: debounce(function () {
      this.loading = true;
      console.log(this.searchValue);
      axios.get(`${API}/search?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.result = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>
