<template>
  <!-- todo focus placeholder -->
  <input 
    id="search" 
    name="search" 
    :class="{ dark : dark }" 
    :value="value" 
    @input="handleChange"
  >
</template>

<script lang="ts">
import { Component, Vue, Prop, Emit } from "vue-property-decorator";

@Component({
  components: {}
})
export default class SearchInput extends Vue {
  @Prop(String) value!: string;
  @Prop({ default: false }) dark!: boolean;

  @Emit("input")
  handleChange(event: any) {
    return event.target.value;
  }
}
</script>

<style lang="scss" scoped>
input {
  margin-top: 50px;
  display: flex;
  flex-direction: column;
  width: 250px;
  color: white;
  text-align: center;
  font-size: 18px;
  font-weight: 300;
  height: 30px;
  border: 0;
  background: none;
  border-bottom: 1px solid white;
  transition: box-shadow 0.3s ease-out;

  @media (min-width: 1024px) {
    font-weight: 400;
  }
}

input:focus {
  outline: none;
  box-shadow: 0 10px 20px -8px rgba(255, 255, 255, 0.5);
}

.dark {
  color: #1e3d4a;
  border-bottom-color: #1e3d4a;
}

dark:focus {
  border-bottom-color: #1e3d4a;
  box-shadow: 0 10px 20px -8px rgba(#1e3d4a, 0.2);
}
</style>