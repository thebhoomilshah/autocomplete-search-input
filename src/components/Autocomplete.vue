<template>
  <div>
    <!-- We can also break this in two components but it is mentioned that need to create only one component so didn't  -->
    <input 
      type="text" class="input" 
      v-model="searchString" 
      :placeholder="placeholder"
      @input="event => {searchString = event.target.value; searchItems()}" 
    />
    <div style="margin-top:-5px"> 
      <div class="item" v-for="(item, index) in filteredItems" :key="index">
        <p @click="clickItem(item)">{{ item.TextField }}</p>
      </div>
    </div>
  </div>
</template>

<script lang="ts">

import { defineComponent } from 'vue';
import Item from "../types/Item";

export default defineComponent({
  name: 'Autocomplete',
  props: {
    items: { 
      type: Object as ()=> Item,
      required:true
    } ,
    placeholder:{
      type:String,
      required:true
    }
  },
  data(){
    return {
      searchString:"" as string|null,
      filteredItems:[] as Item[],
      selectedItem : {} as Item
    }
  },
  methods:{
    clickItem(item:Item){
      this.searchString = item.TextField;
      this.selectedItem = item
      this.filteredItems = []
    },
    searchItems() {
      this.filteredItems = []
      for (let [ key, value ] of Object.entries(this.items)) {
        // additional condition to avoid searchString=null
        if(this.searchString && value.TextField.toLowerCase().indexOf(this.searchString.toLowerCase()) > -1){
          this.filteredItems.push(value)
        }
      }
    }
  }
});
</script>
<style scoped>
.input{
  width: 100%;
  max-width: 320px;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
}
.item{
  width: 100%;
  max-width: 320px;
  text-align:center;
  border-bottom:solid 1px #eee;
  padding:.1px;
  margin:auto;
  background: #fff;
}
</style>