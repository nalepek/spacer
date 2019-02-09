<template>
  <div :style="style" class="item">
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from "vue-property-decorator";

@Component({
  components: {}
})
export default class Item extends Vue {
  @Prop(Object)
  item!: any;

  photo: string = this.item.links[0].href;
  title: string = this.item.links[0].title;

  style = {
      backgroundImage: `url("${this.photo}")`
  }
}
</script>

<style lang="scss" scoped>
    .item {
        width: 40vw;
        height: 250px;
        background-size: cover;
        background-repeat: no-repeat;
        background-position: 50%;

        @media (min-width: 768px){
            width: 25vw;
        }
    }
</style>