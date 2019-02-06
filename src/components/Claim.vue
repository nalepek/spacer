<template>
  <div class="claimWrapper">
    <h1 class="claim">SPACER</h1>
    <p class="subclaim">
      Begin your journey through our amazing galaxy,
      and discover places you never ever heard of.
    </p>
    <p class="subclaim">Type anything sapce-related to start.</p>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component({
  components: {}
})
export default class Claim extends Vue {}
</script>

<style lang="scss" scoped>
.claimWrapper {
  display: -webkit-flex;
  display: -webkit-box;
  display: -moz-flex;
  display: -moz-box;
  display: -ms-flexbox;
  display: flex;
  text-align: center;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.claim {
  font-size: 50px;
  margin: 0;
}

.subclaim {
  margin: 20px 0 0 0;
  font-size: 13px;
}
</style>
