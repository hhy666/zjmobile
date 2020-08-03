<template>
  <view class='cpxgk'>
      <view class="cpxgk_part_1" >
        <text class="cpxgk_part_1_title" >{{cpxgkPart1Title}}</text>
        <view class="cpxgk_chart_gd" >
          <chart :option="gdOption" />
        </view>
      </view>
      <view class="cpxgk_part_2" >
        <text class="cpxgk_part_2_title" >{{cpxgkPart2Title}}</text>
        <view class="cpxgk_chart_je" >
          <chart :option="jeOption" />
        </view>
      </view>
      <view class="cpxgk_part_3" >
        <text class="cpxgk_part_3_title" >{{cpxgkPart3Title}}</text>
        <view class="cpxgk_chart_cz" >
          <chart :option="czOption" />
        </view>
      </view>
      <view class="cpxgk_part_4" >
        <text class="cpxgk_part_4_title" >{{cpxgkPart4Title}}</text>
        <view class="cpxgk_chart_kh" >
          <chart :option="khOption" />
        </view>
      </view>
      <view class="cpxgk_part_5" >
        <text class="cpxgk_part_5_title" >{{cpxgkPart5Title}}</text>
        <!-- 各线业务 -->
        <view class="cpxgk_chart_gxyw" >
          
        </view>
      </view>
  </view>
</template>

<script>
import './cpxgk.scss'
import { $ } from '@tarojs/extend'

import chart from "../chart/chart.vue";

export default {
  name: 'cpxgk',
  data(){
    return {
      cpxgkPart1Title:'产品线累计开工单数量TOP5',
      cpxgkPart2Title:'产品线累计完工金额TOP5',
      cpxgkPart3Title:'产品线累计出证数量TOP5',
      cpxgkPart4Title:'产品线累计客户数量TOP5',
      cpxgkPart5Title:'各产品线业务情况',
      gdOption:Object,
      jeOption:Object,
      czOption:Object,
      khOption:Object
    }
  },
  components: {
    chart: chart
  },
  created(){
    let color=['#9CD557','#F2D468','#E86562','#A071E5','#62D8D8'];
    let radius=['50%', '75%'];
    let gdData=[
      {value: 5000, name: '石油化工'},
      {value: 3431, name: '再生资源'},
      {value: 3161, name: '通用线'},
      {value: 7161, name: '矿产品'},
      {value: 4000, name: '商务代理'}
    ];
    this.gdOption = this.initBingOption(color,this.cpxgkPart1Title,radius,170,gdData,false);
    this.initJeOption();

    color=['#578EF2','#F4B65F','#C05AAD','#CF3D7A','#F97E31'];
    radius=['35%', '60%'];
    gdData=[
      {value: 5000, name: '石油化工'},
      {value: 3431, name: '再生资源'},
      {value: 3161, name: '通用线'},
      {value: 7161, name: '矿产品'},
      {value: 4000, name: '商务代理'}
    ];
    this.czOption = this.initBingOption(color,this.cpxgkPart1Title,radius,170,gdData,true);
    this.initKhOption();
  },
  mounted(){},
  methods: {
    initBingOption: function(color,name,radius,startAngle,data,isLegend){
      return {
        backgroundColor:"#fff",
        color:color,
        legend:{
          show:isLegend,
          bottom:10,
          itemWidth:5,
          itemHeight:5,
          data:['石油化工','再生资源','通用线','矿产品','商务代理']
        },
        series: [
            {
                name: name,
                type: 'pie',
                startAngle:startAngle,
                radius: radius,
                center: ['50%', '50%'],
                data: data,
                label:{
                  show: true,
                  formatter: '{b}\n{c}, {d}%',
                  color:'#444',
                  fontSize:12,
                  fontWeight:'bold'
                },
                labelLine:{
                  length:10,
                  length2:15,
                  lineStyle:{
                      color:'#BEBEBE'
                  }  
                },
                itemStyle:{
                    borderWidth:3,
                    borderColor:'#fff'
                },
                emphasis: {
                    itemStyle: {
                        shadowBlur: 10,
                        shadowOffsetX: 0,
                        shadowColor: 'rgba(0, 0, 0, 0.5)'
                    }
                }
            }
        ]
      }
    },
    initJeOption:function (){
      this.jeOption = {
          color:['#1466FC','#F8CBAD'],
          legend: {
              bottom:5,
              data: ['预测收入', '成本']
          },
          grid: {
              top:10,
              left:10,
              right: 20,
              bottom: 40
          },
          xAxis: {
                  type: 'value',
                  axisTick: {
                      show: false
                  },
                  axisLine: {
                      show: false
                  },
                  axisLabel: {
                      show: false
                  }
          },
          yAxis: [
              {
                  type: 'category',
                  offset: -window.innerWidth*0.35,
                  axisTick: {
                      show: false
                  },
                  axisLine: {
                      show: false
                  },
                  axisLabel:{
                    fontWeight:'bold',
                    color:'#fff'
                  },
                  zlevel:2,
                  data: ['再生资源', '通用线', '矿产品', '商务代理', '石油化工']
              },
              {
                  type: 'category',
                  axisTick: {
                      show: false
                  },
                  axisLine: {
                      show: false
                  },
                  axisLabel:{
                    show:false
                  },
                  zlevel:2,
                  data: ['再生资源', '通用线', '矿产品', '商务代理', '石油化工']
              }
          ],
          series: [
              {
                  name: '预测收入',
                  type: 'bar',
                  label: {
                      show: true,
                      position: 'right',
                      color:'#000'
                  },
                  zlevel:1,
                  yAxisIndex:0,
                  barWidth:30,
                  data: [8465, 9000, 11545, 15486, 16458]
              },
              {
                  name: '成本',
                  type: 'bar',
                  label: {
                      show: true,
                      position: 'left',
                      color:'#000'
                  },
                  barGap:"0%",
                  yAxisIndex:1,
                  zlevel:1,
                  barWidth:30,
                  data: [-3431, -2161, -7161, -4000, -5000]
              }
          ]
      }
    },
    initKhOption:function (){
      this.khOption = {
        color:['#00B0F0', '#DEEBF7'],
        legend:{
            show:true,
            icon:'rect',
            bottom:5,
            left:'45%',
            itemWidth:12,
            itemHeight:12,
            data:['客户数量']  
        },
        grid: {
            top:30,
            bottom:60,
            right:20,
            left: '18%'
        },
        xAxis: {
            type: 'value',
            min:0,
            max:10000,
            minInterval:2000,
            maxInterval:2000,
            axisLabel:{
                show:true, 
                formatter:value=>{return value/100+'%'}, 
                margin: 20
            },
            axisTick:{
                show:false  
            },
            axisLine:{
              show:false  
            }
        },
        yAxis: {
            type: 'category',
            axisLabel:{
                align:'right',
                margin: 5
            },
            axisTick:{
                show:false  
            },
            data: ['再生资源', '通用线', '矿产品', '商务代理', '石油化工']
        },
        series: [
            {
                name:'客户数量',
                type: 'bar',
                barWidth:25,
                data: [[3431,0,21.98],[1161,1,19.27],[7161,2,34.51],[4000,3,5.59],[5000,4,23.98]],
                label:{
                    show:true,
                    position:'right',
                    color:'#000',
                    fontWeight:'bold',
                    formatter:function(params){
                        return params.data[0]+'   '+params.data[2]+'%';
                    }
                },
                stack:1,
                z:2
            },
            {
                name:'客户占比',
                type: 'bar',
                barWidth:25,
                data: [10000,10000,10000,10000,10000],
                label:{
                    show:false
                },
                stack:1,
                z:1
            }
        ]
      }
    }
  }
}
</script>
<style lang='scss' scoped>
</style>
