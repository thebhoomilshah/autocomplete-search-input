<template>
  <div id="app">
    <Autocomplete :items="items" placeholder="Search Item" />
  </div>
</template>

<script lang="ts">

import { defineComponent } from 'vue';
import Autocomplete from './components/Autocomplete.vue';
// data types 
import Item from "./types/Item";
import items from "./config/items";

export default defineComponent({
  name: 'App',
  components: {
    Autocomplete
  },
   data() {
    return {
      //We could also define that items here but values are static so I put them in separate file
      items: items as Item[]
    };
  },
});
</script>

<style>
body {
  background : #eee;
}
</style>
