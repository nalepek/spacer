<template>
  <div class="wrapper">
    <div class="search">
      <label for="search">Search</label>
      <input 
        id="search" 
        name="search" 
        v-model="searchValue"
        @input="handleInput"
      />
      <ul>
        <li v-for="item in results" :key="item.data[0].nasa_id">
          <p>
            {{item.data[0].description}}
          </p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import axios from 'axios';
import { debounce } from "lodash";

@Component({
  components: {
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
    width: 100%;
    margin: 0;
    padding: 30px;
  }

  .search {
    display: flex;
    flex-direction: column;
    width: 250px;
  }

  label {
    font-family: Monsterrat, sans-serif;
  }

  input {
    height: 30px;
    border: 0;
    border-bottom: 1px solid black;
  }
</style>
