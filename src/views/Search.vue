<template>
  <div class="wrapper">
    <Claim />
    <SearchInput />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import axios from 'axios';
import { debounce } from "lodash";

@Component({
  components: {
    Claim,
    SearchInput
  },
})
export default class Search extends Vue {

  API : string = 'https://images-api.nasa.gov';

  searchValue : string = '';

  results = [];
  

  private callApi(param : string) {
    axios.get(`${this.API}/search?q=${param}&media_type=image`)
      .then((response) => {
        this.results = response.data.collection.items;
      })
      .catch((error) => {
        console.log(error);
      });
  }

  private debouncedInput = debounce((param: string) => {
    this.callApi(param);
  }, 500);

  handleInput() {
    this.debouncedInput(this.searchValue);
  }

  //   //super();
  // }
}
</script>

<style lang="scss" scoped>
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
    padding: 30px;
    width: 100%;
    height: 100vh;
    justify-content: center;
    background-image: url(../assets/heroimage.jpg);
    background-repeat: no-repeat;
    background-size: cover;
    background-position: 80% 0%;
  }

  
</style>
