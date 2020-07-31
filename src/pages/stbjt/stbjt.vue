<template>
  <view class='stbjt'>
    <view class="stbjt_part_1" >
      <text class="stbjt_part_1_title" >{{stbjtPart1Title}}</text>
      <view class="stbjt_chart_ywcbQs" >
        <chart :option="ywcbQsOption" />
      </view>
    </view>
    <view class="stbjt_part_2" >
      <text class="stbjt_part_2_title" >{{stbjtPart2Title}}</text>
      <view class="stbjt_chart_ywcbBing" >
        <view class="stbjt_chart_ywcbBing_1" >
          <view class="stbjt_chart_ywcbBing_1_chart" >
            <chart :option="ywcbBing1Option" />
          </view>
          <view class="stbjt_chart_ywcbBing_1_text" >
            <view class="scy1t_circle scy1t_bgcolor_1" ></view>
            <text class="scy1t_text" >间接成本<text class="scy1t_text_big" >1.9</text>亿元</text>
          </view>
        </view>
        <view class="stbjt_chart_ywcbBing_2" >
          <view class="stbjt_chart_ywcbBing_1_chart" >
            <chart :option="ywcbBing2Option" />
          </view>
          <view class="stbjt_chart_ywcbBing_1_text" >
            <view class="scy1t_circle scy1t_bgcolor_2" ></view>
            <text class="scy1t_text" >直接成本<text class="scy1t_text_big" >1.45</text>亿元</text>
          </view>
        </view>
      </view>
    </view>  
    <view class="stbjt_part_3" >
      <text class="stbjt_part_3_title" >{{stbjtPart3Title}}</text>
      <view class="stbjt_chart_czBing" >
        <chart :option="czBingOption" />
      </view>
    </view>
    <view class="stbjt_part_4" >
      <text class="stbjt_part_4_title" >{{stbjtPart4Title}}</text>
      <view class="stbjt_chart_zhu" >
        <chart :option="zhuOption" />
      </view>
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
        stbjtPart1Title:'本年业务及成本趋势图',
        stbjtPart2Title:'本年业务成本情况',
        stbjtPart3Title:'本年出证情况',
        stbjtPart4Title:'本年客户情况',
        ywcbQsOption:Object,
        ywcbBing1Option:{},
        ywcbBing2Option:{},
        czBingOption:{},
        zhuOption:{}
    }
  },
  components: {
    chart: chart
  },
  created(){
    this.initYwcbQsOption();
    this.ywcbBing1Option = this.initYwcbBingOption(56, '#007AFF');
    this.ywcbBing2Option = this.initYwcbBingOption(44, '#F5A623');
    this.initCzBingOption();
    this.initZhuOption();
  },
  mounted(){
    
  },
  methods: {
    initYwcbQsOption:function(){
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
      
      this.ywcbQsOption = {
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
    /**
     * percent  显示的百分比
     * clr 文字显示的颜色（圆环颜色）
     */
    initYwcbBingOption:function(percent, clr){
      return {
            color:[clr],  
            angleAxis: {
                show: false,
                max: 100 * 360 / 270, //-45度到225度，二者偏移值是270度除360度
                type: 'value',
                startAngle: 225, //极坐标初始角度
                splitLine: {
                    show: false
                }
            },
            barMaxWidth: 14, //圆环宽度
            radiusAxis: {
                show: false,
                type: 'category',
            },
            //圆环位置和大小
            polar: {
                center: ['50%', '55%'],
                radius: '100'
            },
            series: [{
                type: 'bar',
                data: [{ //上层圆环，显示数据
                    value: 75,
                    itemStyle: {
                        color: clr
                    },
                }],
                barGap: '-100%', //柱间距离,上下两层圆环重合
                coordinateSystem: 'polar', 
                roundCap: true, //顶端圆角
                z: 2 //圆环层级，同zindex
            },
            { //下层圆环，显示最大值
                type: 'bar',
                data: [{
                    value: 100,
                    itemStyle: {
                        color: '#F3F4F8'
                    }
                }],
                barGap: '-100%',
                coordinateSystem: 'polar',
                roundCap: true,
                z: 1
            },
            //仪表盘
            {
                type: 'gauge',
                axisLine: {
                    show: false,
                    lineStyle:{
                        color:[[1,clr]]
                    }
                },
                splitLine: {
                    show: false
                },
                axisTick: {
                    show: false
                },
                axisLabel: {
                    show: false
                },
                splitLabel: {
                    show: false
                },
                pointer: {
                    show: false
                },
                detail: {
                    formatter: '{value}%',
                    fontSize: 25,
                    offsetCenter: ['2%', '15%']
                },
                data: [{
                    value: percent
                }]
            },
            {
                type:'scatter',
                coordinateSystem: 'polar',
                data:[{
                    symbol: 'circle',
                    symbolSize:7,
                    value:75,
                    name:'222'
                }],
                itemStyle:{
                    color:'#fff',
                    opacity: 1
                },
                silent:true,
                z:3
            }
          ]
      }
    },
    initCzBingOption:function(){
      this.czBingOption = {
        backgroundColor:"#fff",
        color:['#00B0F0','#37CD96','#FFC000'],
        series: [
            {
                name: '访问来源',
                type: 'pie',
                startAngle:140,
                radius: ['55', '75'],
                center: ['50%', '50%'],
                data: [
                    {value: 716, name: '其他成果物'},
                    {value: 3431, name: '纸质证书'},
                    {value: 1161, name: '电子证书'}
                ],
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
    initZhuOption:function(){
      this.zhuOption = {
        color:['#00B0F0', '#DEEBF7'],
        legend:{
            show:true,
            icon:'rect',
            left:'40%',
            data:['客户数量','客户占比']  
        },
        grid: {
            top:30,
            bottom:30,
            right:20,
            left: 115
        },
        xAxis: [{
            type: 'value',
            min:0,
            max:500,
            minInterval:100,
            maxInterval:100,
            axisLabel:{
                show:false,  
                margin: 20
            },
            axisTick:{
                show:false  
            },
            axisLine:{
              show:false  
            }
        },{
            type:'category',
            boundaryGap: false,
            data:['100%','100%','100%','100%','100%','100%'],
            position:'bottom',
            axisTick:{
                show:false  
            },
            axisLine:{
              show:false  
            }
        }],
        yAxis: {
            type: 'category',
            inverse:true,
            axisLabel:{
                align:'right',
                margin: 5
            },
            axisTick:{
                show:false  
            },
            data: ['个人客户', '政府及公共组织客户', '检查机构', '公司客户']
        },
        series: [
            {
                name:'客户数量',
                type: 'bar',
                barWidth:25,
                data: [[180,0,1254],[180,1,2161],[180,2,3161],[180,3,9431]],
                label:{
                    show:true,
                    align:'center',
                    formatter:function(params){
                        return params.data[2];
                    }
                },
                stack:1,
                z:2
            },
            {
                name:'客户占比',
                type: 'bar',
                barWidth:25,
                data: [[600,0,'7.83%'],[600,1,'13.50%'],[600,2,'19.75%'],[600,3,'58.92%']],
                label:{
                    show:true,
                    color:'#000',
                    align:'center',
                    formatter:function(params){
                        return params.data[2];
                    }
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
