<template>
  <div class="container">
    <div class="row">
      <template v-for="(item, index) in dataa" :key="index">
        <template v-if="index == 0 || (index + 1) % pageSize == 0">  
          <OneItem :dataa="item" :class="`col-sm-` + bWidth + ` oneItem`" />
        </template>
        <template v-else
          ><OneItem :dataa="item" :class="`col-sm-` + sWidth + ` oneItem`"
        /></template>
      </template>
    </div>
  </div>
</template>

<script>
import OneItem from "./OneItem.vue";
export default {
  data() {
    return {
      bWidth: 8, //for big size component
      sWidth: 4, //for small size component
      pageSize: 7, // num of components in the page
    };
  },
  name: "RowList",
  props: ["dataa"],
  components: {
    OneItem,
  },
  watch: {
    dataa: {
      handler() {
        
        console.log("from RowData", this.dataa); // log the data if it changed
      },
    },
  },
};
</script>

<style scoped>
.oneItem {
  padding-left: 0% !important;
}

@media screen and (max-width: 575px) {
  .oneItem{padding-right: 0% !important;}
}
</style>
