<template>
    <div class="outerWrapper">
        <div class="innerWrapper">
            <div class="photo" :style="style">
                <!-- <div :style="style" class="item"> -->
                <!-- <img :src="photo"> -->
            </div>
            <div class="description">
                <h2 class="title">{{title}}</h2>
                <p>{{description}}</p>
            </div>
        </div>
        <div class="close" @click="$emit('closeModal')">
        </div>
    </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from "vue-property-decorator";

@Component({
  components: {}
})
export default class Modal extends Vue {

    @Prop(Object)
    item: any;

    photo : string = this.item.links[0].href;
    title : string = this.item.data[0].title;
    
    //todo readmore - scroll
    description : string = this.item.data[0].description.substring(0, 200);

    style = {
        backgroundImage: `url("${this.photo}")`
    }
}
</script>

<style lang="scss" scoped>
    .outerWrapper {
    background: #f6f6f6;
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;

    @media (min-width: 1024px) {
        max-width: 70%;
        height: 60%;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        margin: auto;
        box-shadow: 0 30px 30px -10px rgba(0,0,0, .3);
    }
  }
  .close {
    position: absolute;
    width: 30px;
    height: 30px;
    padding: 30px;
    right: 0;
    top: 0;
    cursor: pointer;

    &::before,
    &::after {
        position: absolute;
        top: 30px;
        right: 20px;
        content: '';
        width: 20px;
        height: 2px;
        background: black;
        display: block;
    }

    &::before {
        transform: rotate(45deg);
    }
    &::after {
        transform: rotate(-45deg);
    }
  }
    .innerWrapper {
        display: flex;
        height: 100%;
        padding: 50px;
        justify-content: center;
        align-items: center;
        flex-direction: column;

        @media (min-width: 1024px) {
            flex-direction: row;

        .photo {
            min-width: 50%;
            margin-right: 20px;
      }
    }
    .photo {
        width: 100%;
        height: 100%;
        background: black;
        background-size: cover;
        background-repeat: no-repeat;
        background-position: 50%;

    //   img {
    //     width: 100%;
    //     height: auto;
    //   }
        }
    }
    .description {
        color: #333;
    }

    .title {
       color: #1e3d4a;
    }
</style>