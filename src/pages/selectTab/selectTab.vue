<template>
  <view class='selectTab'>
      <view class="tab" v-for="(item, index) in tabData" :key="index" >
        <a class="text"  v-bind:class="{cur: item.isCur}" @click="changeTab(index)" >{{item.name}}</a>
        <view class="under_line" v-bind:class="{cur: item.isCur}" ></view>
      </view>
  </view>
</template>

<script>
import '../selectTab/selecttab.scss'

export default {
  name: 'selectTab',
  data(){
    return {
        tabData:[{
            name:'集团概况',
            isCur:true
        },
        {
            name:'产品线概况',
            isCur:false
        },{
            name:'机构概况',
            isCur:false
        },{
            name:'客户概况',
            isCur:false
        }]
    }
  },
  components: {},
  created(){},
  mounted(){
      
  },
  methods: {
      changeTab:function(index){
          this.tabData.forEach(item => {
              item.isCur=false;
          });
          this.tabData[index].isCur = true;
      }
  }
}
</script>
<style lang='scss' scoped>
</style>
