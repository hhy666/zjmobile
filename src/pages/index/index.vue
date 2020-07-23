<template>
  <view class="index" >
    <view class="page_top">
      <view class="page_top_back" >{{back}}</view>  
      <view class="page_title" >
        <text>{{ title }}</text>
      </view>
    </view>  
    <view class="page_top_next" >
      <view class="ptn_left" >
        <text class="second_title" >{{title}}</text>
        <text class="data_date" >{{dataDate}}</text>
      </view>
      <view class="ptn_right" >
          <view class="ptn_right_left" >
            <text class="circle" >?</text>
          </view>
          <text class="data_explain" >{{dataExplain}}</text>
      </view>
    </view>
    <view class="today_total_msg" >
      <TodayTotal></TodayTotal>
    </view>
  </view>
</template>

<script>
import './index.scss'
import TodayTotal from '../todayTotal/totadyTotal.vue'

export default {
  data () {
    return {
      back:'<',
      title: '中检一天',
      dataDate: "数据更新截止 " + new Date().toISOString().slice(0,10) + ' ' + new Date().toTimeString().slice(0,8),
      dataExplain: "数据说明"
    }
  },
  components: {
    TodayTotal: TodayTotal
  },
  methods:{
      
  }
}
</script>
