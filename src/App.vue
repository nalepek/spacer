<template>
  <div :class="[{ flexStart: step === 1 }, 'wrapper']">
    <transition name="slide">
      <img src="./assets/logo.svg" class="logo" v-if="step === 1" />
    </transition>
    <transition name="fade">
      <HeroImage v-if="step === 0"/>
    </transition>
    <Claim v-if="step === 0" />
    <SearchInput 
      v-model="searchValue" 
      @input="handleInput" 
      :dark="step === 1"/>
    <div class="results" v-if="results && !loading && step === 1">
      <Item 
        v-for="item in results" 
        :item="item" 
        :key="item.data[0].nasa_id" 
        @click.native="handleModalOpen(item)"/>
    </div>
    <div class="loader" v-if="step === 1 && loading"></div>
    <Modal 
      v-if="modalOpen" 
      :item="modalItem"
      @closeModal="modalOpen = false" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';
import axios from 'axios';
import { debounce } from "lodash";

@Component({
  components: {
    Claim,
    SearchInput,
    HeroImage,
    Item,
    Modal
  },
})
export default class Search extends Vue {

  API : string = 'https://images-api.nasa.gov';

  loading : boolean = false;
  step : number = 0;
  
  searchValue : string = '';
  results = [];

  modalOpen : boolean = false;
  modalItem : any;  

  private callApi(param : string) {
    axios.get(`${this.API}/search?q=${param}&media_type=image`)
      .then((response) => {
        this.results = response.data.collection.items;
        this.loading = false;
        this.step = 1;
      })
      .catch((error) => {
        console.log(error);
      });
  }

  private debouncedInput = debounce((param: string) => {
    this.callApi(param);
  }, 500);

  handleInput() {
    this.loading = true;
    this.debouncedInput(this.searchValue);
  }

  handleModalOpen(item: any){
    this.modalOpen = true;
    this.modalItem = item;
  }
}
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800');
  
  $font-weight-light: 300;
  $font-weight-normal: 400;
  $font-weight-bold: 600;
  $font-weight-black: 800;

  * {
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  body {
    font-family: 'Monsterrat', sans-serif;
    margin: 0;
    padding: 0;
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .3s ease;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  .slide-enter-active, .slide-leave-active {
    transition: margin-top .3s ease;
  }
  .slide-enter, .slide-leave-to {
    margin-top: -50px;
  }

  .wrapper {
    display: -webkit-flex;
    display: -webkit-box;
    display: -moz-flex;
    display: -moz-box;
    display: -ms-flexbox;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0;
    position: relative;
    padding: 30px;
    width: 100%;
    min-height: 100vh;
    justify-content: center;

    &.flexStart {
      justify-content: flex-start;
    }
  }

  .logo {
    position: absolute;
    top: 30px;
  }

  .results {
    margin-top: 50px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;

    @media (min-width: 768px){
      width: 90%;
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
