<template>
  <div class="searchWrapper">
    <input id="search" name="search" v-model="searchValue" @input="handleInput">
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component({
  components: {}
})
export default class SearchInput extends Vue {}
</script>

<<style lang="scss">
  .searchWrapper {
    margin-top: 50px;
    display: flex;
    flex-direction: column;
    width: 250px;
  }
  
  input {
    height: 30px;
    border: 0;
    background: none;
    border-bottom: 1px solid black;
  }
</style>