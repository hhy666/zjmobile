<template>
  <view class='khgk'>
    <view class="khgk_part_1" >
      <text class="khgk_part_1_title" >{{khgkPart1Title}}</text>
      <view class="khgk_chart_khywQs" >
        <chart :option="khywQsOption" />
      </view>
    </view>
    <view class="khgk_part_2" >
      <text class="khgk_part_2_title" >{{khgkPart2Title}}</text>
      <view class="khgk_chart_gskh" >
        <khmsg :option="gskhOption" />
      </view>
    </view>
    <view class="khgk_part_3" >
      <text class="khgk_part_3_title" >{{khgkPart3Title}}</text>
      <view class="khgk_chart_jcjg" >
        <khmsg :option="jcjgOption" />
      </view>
    </view>
    <view class="khgk_part_4" >
      <text class="khgk_part_4_title" >{{khgkPart4Title}}</text>
      <view class="khgk_chart_zfzz" >
        <khmsg :option="zfzzOption" />
      </view>
    </view>
    <view class="khgk_part_5" >
      <text class="khgk_part_5_title" >{{khgkPart5Title}}</text>
      <view class="khgk_chart_gr" >
        <khmsg :option="grOption" />
      </view>
    </view>
    <view class="khgk_part_6" >
      <text class="khgk_part_6_title" >{{khgkPart6Title}}</text>
      <view class="khgk_chart_khgx" >
        <chart :option="khgxOption" />
      </view>
    </view>
  </view>
</template>

<script>
import './khgk.scss'
import { $ } from '@tarojs/extend'
import chart from "../chart/chart.vue"
import khmsg from "../khmsg/khmsg.vue"

export default {
  name: 'khgk',
  data(){
    return {
      khgkPart1Title:'本年客户业务趋势',
      khgkPart2Title:'公司客户',
      khgkPart3Title:'检测机构',
      khgkPart4Title:'政府及组织机构客户',
      khgkPart5Title:'个人客户',
      khgkPart6Title:'本年客户贡献值TOP10',
      khywQsOption:Object,
      gskhOption:Object,
      jcjgOption:Object,
      zfzzOption:Object,
      grOption:Object,
      khgxOption:Object
    }
  },
  components: {
    chart: chart,
    khmsg: khmsg
  },
  created(){
    this.initKhywQsOption();
    
    this.gskhOption = this.initGskhOption(44,'#F5A523',75,{
      year:'4,000',
      month:'400',
      day:'22',
      wtjeNum:'2.46',
      wtjeUnit:'亿元',
      kpsrNum:'2',
      kpsrUnit:'亿元',
      kgdslNum:'2',
      kgdslUnit:'万单',
      czslNum:'2',
      czslUnit:'万份',
      wordColor:'#F5A523'
    });
    
    this.jcjgOption = this.initGskhOption(56,'#0079FF',75,{
      year:'4,000',
      month:'400',
      day:'22',
      wtjeNum:'2.46',
      wtjeUnit:'亿元',
      kpsrNum:'2',
      kpsrUnit:'亿元',
      kgdslNum:'2',
      kgdslUnit:'万单',
      czslNum:'2',
      czslUnit:'万份',
      wordColor:'#0079FF'
    });
    
    this.zfzzOption = this.initGskhOption(56,'#8850BB',52,{
      year:'4,000',
      month:'400',
      day:'22',
      wtjeNum:'2.46',
      wtjeUnit:'亿元',
      kpsrNum:'2',
      kpsrUnit:'亿元',
      kgdslNum:'2',
      kgdslUnit:'万单',
      czslNum:'2',
      czslUnit:'万份',
      wordColor:'#8850BB'
    });
    
    this.grOption = this.initGskhOption(44,'#57CB7D',63,{
      year:'4,000',
      month:'400',
      day:'22',
      wtjeNum:'2.46',
      wtjeUnit:'亿元',
      kpsrNum:'2',
      kpsrUnit:'亿元',
      kgdslNum:'2',
      kgdslUnit:'万单',
      czslNum:'2',
      czslUnit:'万份',
      wordColor:'#57CB7D'
    });

    const yData = [], sdata = [];

    for (let index = 0; index < 10; index++) {
      yData.push('客户客户客');
    }

    sdata.push([5000,4000,7161,3161,3431,5000,4000,7161,3161,3431]);
    sdata.push([50001,40001,71611,31611,34311,50001,40001,71611,31611,34311]);

    this.initKhgxOption(yData, sdata);
  },
  mounted(){},
  methods: {
    initKhywQsOption(){
      const xAxisData = [];

      for (let index = 1; index < 13; index++) {
        xAxisData.push(index+'月');
      }   

      const legendData = [];

      legendData.push({name:'客户数量',icon:'emptyDiamond'});
      legendData.push({name:'委托单',icon:'emptyTriangle'});
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
      
      this.khywQsOption = {
        color:['#9AD35C','#0436EE','#FF0000'],
        legend:[{
          height:20,
          top:10,
          itemWidth:10,
          itemHeight:10,
          data:legendData
        }],
        grid:[{
          left: 40,
          right: 40,
          top: 40,
          bottom: 30
        }],
        xAxis:[{
          type: 'category',
          splitLine: {
            show:false
          },
          axisLabel: {
            interval: 0,
            color:'#333'
          },
          axisTick: {
            show:false,
            alignWithLabel: true
          },
          axisLine:{
            lineStyle:{
              color:'#ccc'
            }
          },
          data:xAxisData
        }],
        yAxis:[{
          position:'left',
          axisLabel: {
            interval: 0,
            color:'#aaa'
          },
          splitLine: {
            show:false
          },
          axisLine:{
            show:false
          }, 
          axisTick: {
            show:false
          },
          min:0,
          max:1200,
          minInterval:200,
          maxInterval:200,
          boundaryGap:300
        },{
          position:'right',
          axisLine:{
            show:false
          }, 
          axisTick: {
            show:false
          },
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
    initYwcbBingOption:function(percent, clr, len){
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
                radius: '90'
            },
            series: [{
                type: 'bar',
                data: [{ //上层圆环，显示数据
                    value: len,
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
                    value:len,
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
    initGskhOption(num,color,len,msg){
      return {
        khmsgOption:this.initYwcbBingOption(num,color,len),
        year:msg.year,
        month:msg.month,
        day:msg.day,
        wtjeNum:msg.wtjeNum,
        wtjeUnit:msg.wtjeUnit,
        kpsrNum:msg.kpsrNum,
        kpsrUnit:msg.kpsrUnit,
        kgdslNum:msg.kgdslNum,
        kgdslUnit:msg.kgdslUnit,
        czslNum:msg.czslNum,
        czslUnit:msg.czslUnit,
        wordColor:msg.wordColor
      }      
    },
    initKhgxOption(yData, sdata){
      this.khgxOption = {
        backgroundColor:'#fff',
        color:['#36C8B5', '#00B0F0'],
        legend:{
          icon:'rect',
          itemWidth:13,
          itemHeight:13,
          bottom:5,
          data:['已到款','贡献值']
        },
        grid: {
            top:10,
            bottom:55,
            right:20,
            left: '18%'
        },
        xAxis: {
            type: 'value',
            min:0,
            max:90000,
            minInterval:20000,
            maxInterval:20000,
            axisLabel:{
              show:true
            },
            axisTick:{
              show:false  
            },
            axisLine:{
              show:false  
            },
            splitLine:{
              lineStyle:{
                color:['#eee']
              }
            }
        },
        yAxis: {
            type: 'category',
            axisLabel:{
                align:'right',
                margin: 5,
                color:'#aaa',
                fontWeight: 'bold'
            },
            axisTick:{
                show:false  
            },
            axisLine:{
                show:true  
            },
            data: yData
        },
        series: [
            {
              name:'已到款',
              type: 'bar',
              barWidth:10,
              barGap:0,
              data: sdata[0],
              label:{
                  show:true,
                  position:'right',
                  color:'#000',
                  verticalAlign:'middle',
                  fontWeight:'bold',
                  offset:[5,0]
              },
              z:2
            },
            {
              name:'贡献值',
              type: 'bar',
              barWidth:10,
              barGap:0,
              data: sdata[1],
              label:{
                  show:true,
                  position:'right',
                  color:'#000',
                  verticalAlign:'middle',
                  fontWeight:'bold',
                  offset:[5,0]
              },
              z:2
            }
        ]
      }      
    }
  }
}
</script>
<style lang='scss' scoped>
</style>
