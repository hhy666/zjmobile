<template>
  <view class='charts' :id="ecid">
    
  </view>
</template>

<script>
import './chart.scss'
import { $ } from '@tarojs/extend'
import * as echarts from "../../ec-canvas/echarts.min.js";

export default {
  name: 'charts',
  data(){
    return {
        ecid: String
    }
  },
  props:{
      option: Object
  },
  components: {
     
  },
  created(){
    this.ecid = new Date().getTime();
  },
  mounted(){
      this.createEcharts();
  },
  methods: {
    createEcharts: function(){
      const chart = echarts.init(document.getElementById(this.ecid));

      chart.setOption(this.option);
    }
  }
}

</script>
<style lang='scss' scoped>
</style>
