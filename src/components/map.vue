<template>
  <div class="hello" id="mainmap">

  </div>
</template>

<script>
  import echarts from 'echarts'
  var hyq=require('../assets/js/hyq.json')
 export default{
     data(){
         return{

         }
     },
   mounted() {

       echarts.registerMap('hyq', hyq);
       var chart = echarts.init(document.getElementById('mainmap'));
       chart.setOption({
         series: [{
           type: 'map',
           map: 'hyq'
         }]
       });


   }
 }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .hello{height: 100%;width: 100%;}
</style>
