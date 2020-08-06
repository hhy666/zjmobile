<template>
  <view class='jggk'>
    <view class="jggk_part_1" >
      <text class="jggk_part_1_title" >{{jggkPart1Title}}</text>
      <view class="jggk_chart_wgje" >
        <chart :option="wgjeOption" />
      </view>
    </view>
    <view class="jggk_part_2" >
      <text class="jggk_part_2_title" >{{jggkPart2Title}}</text>
      <view class="jggk_chart_czsl" >
        <chart :option="czslOption" />
      </view>
    </view>
    <view class="jggk_part_3" >
      <text class="jggk_part_3_title" >{{jggkPart3Title}}</text>
      <view class="jggk_chart_khsl" >
        <chart :option="khslOption" />
      </view>
    </view>
    <view class="jggk_part_4" >
      <text class="jggk_part_4_title" >{{jggkPart4Title}}</text>
      <a class="jp4_tab_1" @click="changeGsDataType(1)" :class="{choosed:curType == 1}" >按公司</a>
      <a class="jp4_tab_2" @click="changeGsDataType(2)" :class="{choosed:curType == 2}" >按区域公司</a>
      <view class="jggk_chart_ywqk" >
        <jgywTable :tableData="gsTableData" />
      </view>
    </view>
  </view>
</template>

<script>
import './jggk.scss'
import { $ } from '@tarojs/extend'

import chart from '../chart/chart.vue';
import jgywTable from '../jgywTable/jgywTable'

export default {
  name: 'jggk',
  data(){
    return {
      jggkPart1Title:'公司累计完工金额TOP10',
      jggkPart2Title:'公司累计出证数量TOP10',
      jggkPart3Title:'公司累计客户数量TOP10',
      jggkPart4Title:'各机构业务情况',
      wgjeOption:Object,
      czslOption:Object,
      khslOption:Object,
      gsTableData:Object,
      curType:1
    }
  },
  components: {
    chart: chart,
    jgywTable: jgywTable
  },
  created(){
    const wgjeYData = ['广东公司','深圳公司','河北公司','河南公司','北京公司','湖南公司','天津公司','辽宁公司','江苏公司'];
    const wgjeSeriesData1 = [], wgjeSeriesData2 = [];
    
    for (let index = 0; index < 10; index++) {
      const mr = parseInt(Math.random()*50000 + 5000);
      wgjeSeriesData1.push(mr + parseInt(Math.random()*30000));
      wgjeSeriesData2.push(-mr);
    }

    this.initWgjeOption(wgjeYData,wgjeSeriesData1,wgjeSeriesData2);

    const sdata = [8465,9000,11545,15486,16458,20246,34655,40665,56686,65987];

    this.initCzslOption(wgjeYData, sdata);
    this.initKhslOption();
    this.initGsTableData(1);
  },
  mounted(){},
  methods: {
    initWgjeOption(yData,sData1,sData2){
      this.wgjeOption = {
        color:['#1466FC','#F8CBAD'],
        legend: {
            bottom:5,
            data: ['成本', '预测收入']
        },
        grid: {
            top:10,
            left:10,
            right: 20,
            bottom: 50
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
                    show: true,
                    formatter:value=>{return value/1000+'%'} 
                },
                min:-80000,
                max:100000,
                minInterval:20000,
                maxInterval:20000
        },
        yAxis: [
            {
                type: 'category',
                offset: -window.innerWidth*0.5,
                axisTick: {
                    show: false
                },
                axisLine: {
                    show: false
                },
                axisLabel:{
                  fontWeight:'bold'
                },
                zlevel:2,
                data: yData
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
                data: yData
            }
        ],
        series: [
            {
                name: '预测收入',
                type: 'bar',
                label: {
                    show: true,
                    position: 'right',
                    color:'#000',
                    fontWeight:'bold'
                },
                zlevel:1,
                yAxisIndex:0,
                barWidth:15,
                data: sData1
            },
            {
                name: '成本',
                type: 'bar',
                label: {
                    show: true,
                    position: 'left',
                    color:'#000',
                    fontWeight:'bold'
                },
                barGap:"0%",
                yAxisIndex:1,
                zlevel:1,
                barWidth:15,
                data: sData2
            }
        ]
      }
    },
    initCzslOption(yData, sdata){
      this.czslOption = {
        color:['#00B0F0'],
        grid: {
            top:5,
            bottom:10,
            right:20,
            left: '18%'
        },
        xAxis: {
            type: 'value',
            min:0,
            max:70000,
            axisLabel:{
              show:false
            },
            axisTick:{
              show:false  
            },
            axisLine:{
              show:false  
            },
            splitLine:{
              show: false
            }
        },
        yAxis: {
            type: 'category',
            axisLabel:{
                align:'right',
                margin: 5,
                color:'#ccc',
                fontWeight: 'bold'
            },
            axisTick:{
                show:false  
            },
            axisLine:{
                show:false  
            },
            data: yData
        },
        series: [
            {
                type: 'bar',
                barWidth:25,
                data: sdata,
                label:{
                    show:true,
                    position:'insideRight',
                    color:'#fff',
                    verticalAlign:'middle',
                    fontWeight:'bold',
                    offset:[5,0]
                },
                stack:1,
                z:2
            }
        ]
      }
    },
    initKhslOption(){
      this.khslOption = {
        backgroundColor:'#fff',
        color:['#FF715D','#37BBF6', '#465668','#35D79A','#F6FC14','#92D050','#3F6CFE','#0234EE','#F389E6','#FFC000'],
        series: [
            {
                type: 'pie',
                radius: '65%',
                center: ['50%', '50%'],
                itemStyle:{
                    borderColor:'#fff',
                    borderWidth:5
                },
                label:{
                  show: true,
                  formatter: '{b}\n{c}, {d}%',
                  color:'#444',
                  fontSize:12,
                  fontWeight:'bold'
                },
                data: [
                    {value: 8465,name: '广东公司'},
                    {value: 9000, name: '深圳公司'},
                    {value: 11545, name: '河北公司'},
                    {value: 15486, name: '河南公司'},
                    {value: 16458, name: '北京公司'},
                    {value: 20246,name: '上海公司'},
                    {value: 34655, name: '湖南公司'},
                    {value: 40665, name: '天津公司'},
                    {value: 46686, name: '辽宁公司'},
                    {value: 65987, name: '江苏公司'}
                ]
            }
        ]
      }
    },
    initGsTableData(type){
      // 在京单位
      const zjdwAry = [], dfgsAry = [], jwgsAry = [],
        len = parseInt(Math.random()*20)+3,
        len1 = parseInt(Math.random()*30)+3,
        len2 = parseInt(Math.random()*40)+3;
      let hj = 0, hj1 = 0, hj2 = 0, hj3 = 0;

      for (let index = 0; index < len; index++) {
        const sj = this.returnRandom(10000),
          sj1 = this.returnRandom(1000),
          sj2 = this.returnRandom(10000),
          sj3 = this.returnRandom(100000);

        hj+=sj;hj1+=sj1;hj2+=sj2;hj3+=sj3;

        zjdwAry.push({
          gsmc:(type==1 ? '在京单位' : '欧洲公司') +index,
          ycsr:sj,
          cb:sj1,
          zss:sj2,
          khs:sj3
        });        
      }

      zjdwAry.push({
        gsmc:'合计',
        ycsr:hj,
        cb:hj1,
        zss:hj2,
        khs:hj3
      });

      hj = 0; hj1 = 0; hj2 = 0; hj3 = 0;

      for (let index = 0; index < len1; index++) {
        const sj = this.returnRandom(10000),
          sj1 = this.returnRandom(1000),
          sj2 = this.returnRandom(10000),
          sj3 = this.returnRandom(100000);

        hj+=sj;hj1+=sj1;hj2+=sj2;hj3+=sj3;

        dfgsAry.push({
          gsmc:(type==1 ? '地方单位' : '东南亚公司')+index,
          ycsr:sj,
          cb:sj1,
          zss:sj2,
          khs:sj3
        });        
      }
      
      dfgsAry.push({
        gsmc:'合计',
        ycsr:hj,
        cb:hj1,
        zss:hj2,
        khs:hj3
      });

      hj = 0; hj1 = 0; hj2 = 0; hj3 = 0;


      for (let index = 0; index < len2; index++) {
        const sj = this.returnRandom(10000),
          sj1 = this.returnRandom(1000),
          sj2 = this.returnRandom(10000),
          sj3 = this.returnRandom(100000);

        hj+=sj;hj1+=sj1;hj2+=sj2;hj3+=sj3;

        jwgsAry.push({
          gsmc:(type==1 ? '境外公司' : '非洲公司')+index,
          ycsr:sj,
          cb:sj1,
          zss:sj2,
          khs:sj3
        });        
      }

      jwgsAry.push({
        gsmc:'合计',
        ycsr:hj,
        cb:hj1,
        zss:hj2,
        khs:hj3
      });

      this.gsTableData = {
        gsTypeAry:type == 1 ? ['在京单位','地方单位','境外公司'] : ['欧洲公司','东南亚公司','非洲公司'],
        curIndex:0,
        zjdwAry:zjdwAry,
        dfgsAry:dfgsAry,
        jwgsAry:jwgsAry,
        gsDataAry:zjdwAry
      }
    },
    returnRandom(max){
      return parseInt(Math.random()*max);
    },
    changeGsDataType(type){
      this.curType = type;
      this.initGsTableData(type);
    }
  }
}
</script>
<style lang='scss' scoped>
</style>
