<template>
  <view class='jgywTable'>
      <view class="t_left" >
          <text class="tl_head" >公司类型</text>
          <a class="tl_tr" 
            v-for="(item,index) in tableData.gsTypeAry" 
            :key="index" 
            :class="{cur:index == tableData.curIndex}" 
            @click="changeGsType(index)">
              {{item}}
          </a>
      </view>
      <view class="t_right" >
          <view class="tr_head" >
            <text class="tr_th_gsmc" >公司名称</text>
            <text class="tr_th_ycsr" >预测收入</text>
            <text class="tr_th_cb" >成本</text>
            <text class="tr_th_zss" >证书数</text>
            <text class="tr_th_khs" >客户数</text>
          </view>
          <view class="tr_tr" v-for="(item,index) in tableData.gsDataAry" :key="index" >
              <text class="tr_td_gsmc" :class="{last: index == tableData.gsDataAry.length - 1}" >{{item.gsmc}}</text>
              <text class="tr_td_ycsr" :class="{last: index == tableData.gsDataAry.length - 1}" >{{item.ycsr}}</text>
              <text class="tr_td_cb" :class="{last: index == tableData.gsDataAry.length - 1}" >{{item.cb}}</text>
              <text class="tr_td_zss" :class="{last: index == tableData.gsDataAry.length - 1}" >{{item.zss}}</text>
              <text class="tr_td_khs" :class="{last: index == tableData.gsDataAry.length - 1}" >{{item.khs}}</text>
          </view>
      </view>
  </view>
</template>

<script>
import './jgywTable.scss'

export default {
  name: 'jgywTable',
  data(){
    return {}
  },
  props:{
      tableData:Object
  },
  components: {},
  created(){},
  mounted(){},
  methods: {
    changeGsType(idx){
        this.tableData.curIndex = idx;
        this.tableData.gsDataAry = idx == 0 ? 
            this.tableData.zjdwAry 
            : (idx == 1 ? this.tableData.dfgsAry
            : this.tableData.jwgsAry);
    }
  }
}
</script>
<style lang='scss' scoped>
*{
    justify-content: center;
    align-items: center;
}

.jgywTable{
    justify-content: start;
    align-items: flex-start;
}

.t_left{
    justify-content: start;
}
</style>
