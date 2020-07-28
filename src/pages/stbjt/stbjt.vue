<template>
  <view class='stbjt'>
      <text class="stbjt_title" >{{stbjtTitle}}</text>
      <view class="stbjt_chart" >
        <chart :option="option" />
      </view>
  </view>
</template>

<script>
import './stbjt.scss'
import { $ } from '@tarojs/extend'

import chart from "../chart/chart.vue";

export default {
  name: 'stbjt',
  data(){
    return {
        stbjtTitle:'本年业务及成本趋势图',
        option:Object
    }
  },
  components: {
    chart: chart
  },
  created(){
    const xAxisData = [];

    for (let index = 1; index < 13; index++) {
      xAxisData.push(index+'月');
    }   

    const legendData = [];

    legendData.push({name:'委托单量',icon:'emptyDiamond'});
    legendData.push({name:'成本',icon:'emptyTriangle'});
    legendData.push({name:'预测收入',icon:'emptyRect'});

    const seriesData = [];

    for (let index = 0; index < legendData.length; index++) {
      const dta = [];

      for (let i = 1; i < 13; i++) {
        dta.push(parseInt(Math.random()*1200));
      }

      seriesData.push({
        name: legendData[index].name,
        type: 'line',
        symbol: index % 3 == 0 ? 'emptyDiamond' : (index % 3 == 2 ? 'emptyRect' : 'emptyTriangle'),
        symbolSize: 8,
        data: dta
      });
    }
    
    this.option = {
        legend:[{
          height:20,
          top:20,
          itemWidth:10,
          itemHeight:10,
          data:legendData
        }],
        grid:[{
          left: 40,
          right: 40,
          top: 50,
          bottom: 60
        }],
        xAxis:[{
          type: 'category',
          splitLine: {
            show:false
          },
          axisLabel: {
            interval: 0
          },
          axisTick: {
            alignWithLabel: true
          },
          data:xAxisData
        }],
        yAxis:[{
          position:'left',
          min:0,
          max:1200,
          minInterval:200,
          maxInterval:200,
          boundaryGap:300
        },{
          position:'right',
          min:0,
          max:7000,
          minInterval:1000,
          maxInterval:1000,
          boundaryGap:300
        }],
        series:seriesData
      }
  },
  mounted(){
    
  },
  methods: {
    
  }
}
</script>
<style lang='scss' scoped>
</style>
