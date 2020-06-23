<template>
  <div class="index">
    <search v-on:handleKeyUp="handleKeyUp"></search>
  </div>
</template>

<script>
  import search from '@c/search.vue'
  export default {
    name: "index",
    components:{
      search
    },
    data(){
      return{
        searchid:''
      }
    },
    methods:{
      handleKeyUp:function (val) {
        this.searchid = val;
      }
    }
  }
</script>

<style lang="scss" scoped>
</style>
