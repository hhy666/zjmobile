<template>
  <view class="page_top">
    <view class="page_top_back" >
      <button>{{back}}</button>
    </view>  
    <view class="page_title" >
      <text>{{ title }}</text>
    </view>
  </view>
</template>

<script>
import './index.scss'

export default {
  data () {
    return {
      back:'\<',
      title: '中检一天'
    }
  }
}
</script>
