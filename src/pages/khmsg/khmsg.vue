<template>
  <view class='khmsg'>
    <view class="khmsg_chart" >
        <chart :option="khmsgOption" />
    </view>
    <view class="khmsg_ymd" >
        <view class="khmsg_year" >本年客户数 <view class="year" :style="{color: this.option.wordColor}" >{{option.year}}</view>个</view>
        <text class="khmsg_month" >本月客户数 <text class="month" :style="{color: this.option.wordColor}" >{{option.month}}</text>个</text>
        <text class="khmsg_day" >今日 + <text class="day" >{{option.day}}</text>个</text>
    </view>
    <view class="khmsg_wkkc" >
        <text class="wkkc_head" >委托金额</text>
        <text class="wkkc_head" >开票收入</text>
        <text class="wkkc_head" >开工单数量</text>
        <text class="wkkc_head" >出证数量</text>
        <text class="wkkc_body" >
            <text class="wkkc_body_num" >{{option.wtjeNum}}</text>
            <text class="wkkc_body_unit" >{{option.wtjeUnit}}</text>
        </text>
        <text class="wkkc_body" >
            <text class="wkkc_body_num" >{{option.kpsrNum}}</text>
            <text class="wkkc_body_unit" >{{option.kpsrUnit}}</text>
        </text>
        <text class="wkkc_body" >
            <text class="wkkc_body_num" >{{option.kgdslNum}}</text>
            <text class="wkkc_body_unit" >{{option.kgdslUnit}}</text>
        </text>
        <text class="wkkc_body" >
            <text class="wkkc_body_num" >{{option.czslNum}}</text>
            <text class="wkkc_body_unit" >{{option.czslUnit}}</text>
        </text>
    </view>
  </view>
</template>

<script>
import './khmsg.scss'
import {$} from '@tarojs/extend'
import chart from '../chart/chart'

export default {
  name: 'khmsg',
  data(){
    return {
        cid:String,
        khmsgOption:Object
    }
  },
  props:{
      option:Object
  },
  components: {
      chart: chart
  },
  created(){
    this.khmsgOption = this.option.khmsgOption;
  },
  mounted(){},
  methods: {}
}
</script>
<style lang='scss' scoped>
*{
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>
