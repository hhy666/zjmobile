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
      dataDate: "数据更新截止 " + this.dateFormat(new Date()),
      dataExplain: "数据说明"
    }
  },
  components: {
    TodayTotal: TodayTotal
  },
  methods:{
      //时间格式化函数，此处仅针对yyyy-MM-dd hh:mm:ss 的格式进行格式化
      dateFormat(time) {
          var date=new Date(time);
          var year=date.getFullYear();
          /* 在日期格式中，月份是从0开始的，因此要加0
            * 使用三元表达式在小于10的前面加0，以达到格式统一  如 09:11:05
            * */
          var month= date.getMonth()+1<10 ? "0"+(date.getMonth()+1) : date.getMonth()+1;
          var day=date.getDate()<10 ? "0"+date.getDate() : date.getDate();
          var hours=date.getHours()<10 ? "0"+date.getHours() : date.getHours();
          var minutes=date.getMinutes()<10 ? "0"+date.getMinutes() : date.getMinutes();
          var seconds=date.getSeconds()<10 ? "0"+date.getSeconds() : date.getSeconds();
          // 拼接
          return year+"-"+month+"-"+day+" "+hours+":"+minutes+":"+seconds;
      }
  }
}
</script>
