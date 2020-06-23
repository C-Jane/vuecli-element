<template>
  <div class="head">
    <div class="tianmei-logo pos-c-t"></div>
    <label for="search" class="search pos-c-t" @click="searchLable"></label>
    <div :class="[isSearch ? 'on': '','serch-input pos-c-t']"><input @blur="isblur" @keyup.13 = "handleKeyUp" type="text" id="search" placeholder="请输入搜索关键词" v-model="searchid"></div>
    <div :class="[isSearch ? 'on': '','hisrorySearch']" v-show="localSearch.length >0">
      <ul>
        <li v-for="(item ,index) in localSearch" :key ='index' @click="searchHis(item)">{{item}}</li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  name: 'search',
  data () {
    return {
      searchid:'',
      isSearch:false,
      localSearch:[]
    }
  },
  created(){
    this.localSearch = JSON.parse(localStorage.getItem('localSearch')) || [];
  },
  methods:{
    searchLable(){
      this.isSearch = true
    },
    isblur(){
      let _this = this
      setTimeout(function () {
        _this.isSearch = false
      },100)
    },
    searchHis(item){
      if(item){this.searchid = item};
      this.handleKeyUp()
    },
    handleKeyUp(){
      let localSearch = this.localSearch;
      let searchid = this.searchid;
      if(!localSearch.includes(searchid)){
        localSearch.push(searchid);
      }
      localStorage.setItem('localSearch',JSON.stringify(localSearch))
      this.$emit('handleKeyUp',searchid)
      this.searchid = ' '
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  @import "@/assets/styles/comm.scss";
  .hisrorySearch{
    position: absolute;
    left:0;
    top:0.85rem;
    width: 100%;
    font-size: .24rem;
    height: 0;
    overflow: hidden;
    &.on{
      height: auto;
    }
    ul{
      display: flex;
      padding: 0.3rem 0;
      flex-wrap: wrap;
    }
    li{
      color: #e0dfdf;
      padding: 0.05rem 0.2rem;
      border-radius: 0.3rem;
      margin-left: .3rem;
      min-width: 0.8rem;
      border: 0.02rem solid #e0dfdf;
    }
  }
</style>
