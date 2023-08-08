<script>
import HeaderView from "./components/header.vue"
import ExChangeView from "./components/ExChange.vue"


export default{
  components:{
    HeaderView,
    ExChangeView
  },
  data() {
    return {
      dataList:[],
      
      
      
    }
  },
  methods: {
   
    
  },
  //生命週期
  mounted() {
    fetch("https://open.exchangerate-api.com/v6/latest")
      .then(res => res.json())
      .then(data => {
        this.dataList = data.rates
        // console.log(this.dataList);
        console.log(data);
      })
      
  },


}


</script>

<template>
  <HeaderView />
  <ExChangeView v-bind:rate="dataList"/>
  <!-- <p v-for="(item,index) in dataList">{{ index }}</p> -->

</template>

<style scoped>

</style>
