<template>
  <view class='cpxywTable'>
      <view class="table_head" >
        <text class="head_1" >一级产品线</text>
        <text class="head_2" >二级产品线</text>
        <text class="head_3" >预测收入</text>
        <text class="head_4" >成本</text>
        <text class="head_5" >证书数</text>
        <text class="head_6" >客户数</text>
      </view>
      <view class="table_body" v-for="(item,index) in cpxData" :key="index" :style="{height:item.tcpxData.length*41+'px'}" >
        <text class="table_body_ocpx bg_color" :style="{height:item.tcpxData.length*41+'px'}" >{{item.olcpxName}}</text>
        <view class="table_body_tcpx" :style="{height:item.tcpxData.length*41+'px'}" >
          <a class="td_tlcpx" v-for="(el,i) in item.tcpxData" :key="i" v-if="i<item.tcpxData.length - 1" >{{el.tlcpxName}}</a>
          <text class="td_tlcpx bg_color" >合计</text>
        </view>
        <view class="table_body_ycsr" :style="{height:item.tcpxData.length*41+'px'}" >
          <text class="td_ycsr" v-for="(el,i) in item.tcpxData" :key="i" 
            :class="{bg_color:i == item.tcpxData.length - 1}" >
            {{el.ycsr}}
          </text>
        </view>
        <view class="table_body_cb" :style="{height:item.tcpxData.length*41+'px'}" >
          <text class="td_cb" v-for="(el,i) in item.tcpxData" :key="i" 
            :class="{bg_color:i == item.tcpxData.length - 1}" >
            {{el.cb}}
          </text>
        </view>
        <view class="table_body_zss" :style="{height:item.tcpxData.length*41+'px'}" >
          <text class="td_zss" v-for="(el,i) in item.tcpxData" :key="i" 
            :class="{bg_color:i == item.tcpxData.length - 1}" >
            {{el.zss}}
          </text>
        </view>
        <view class="table_body_khs" :style="{height:item.tcpxData.length*41+'px'}" >
          <text class="td_khs" v-for="(el,i) in item.tcpxData" :key="i" 
            :class="{bg_color:i == item.tcpxData.length - 1}" >
            {{el.khs}}
          </text>
        </view>
      </view>
  </view>
</template>

<script>
import './cpxywTable.scss'
import {$} from '@tarojs/extend'

export default {
  name: 'cpxywTable',
  data(){
    return {
      cpxData:Array
    }
  },
  components: {},
  created(){
    this.cpxData = [];
    this.cpxData.push({
      olcpxName:'大宗贸易',
      tcpxData:[{
        tlcpxName:'矿产品',
        ycsr:'24,600万',
        cb:'1088万',
        zss:'1088万',
        khs:'2000万'
      },{
        tlcpxName:'石油化石',
        ycsr:'24,600万',
        cb:'1088万',
        zss:'1088万',
        khs:'2000万'
      },{
        tlcpxName:'合计',
        ycsr:'59,200万',
        cb:'2176万',
        zss:'2176万',
        khs:'4000万'
      }]
    },{
      olcpxName:'农食安全及溯源',
      tcpxData:[{
        tlcpxName:'农食安全',
        ycsr:'246万',
        cb:'188万',
        zss:'188万',
        khs:'2万'
      },{
        tlcpxName:'智慧农业',
        ycsr:'246万',
        cb:'188万',
        zss:'188万',
        khs:'2万'
      },{
        tlcpxName:'溯源服务',
        ycsr:'246万',
        cb:'188万',
        zss:'188万',
        khs:'2万'
      },{
        tlcpxName:'合计',
        ycsr:'738万',
        cb:'564万',
        zss:'564万',
        khs:'6万'
      }]
    },{
      olcpxName:'工业',
      tcpxData:[{
        tlcpxName:'工程监造',
        ycsr:'246万',
        cb:'188万',
        zss:'188万',
        khs:'2万'
      },{
        tlcpxName:'设备监理',
        ycsr:'246万',
        cb:'188万',
        zss:'188万',
        khs:'2万'
      },{
        tlcpxName:'计量校准',
        ycsr:'246万',
        cb:'188万',
        zss:'188万',
        khs:'2万'
      },{
        tlcpxName:'合计',
        ycsr:'738万',
        cb:'564万',
        zss:'564万',
        khs:'6万'
      }]
    },{
      olcpxName:'消费品',
      tcpxData:[{
        tlcpxName:'纺织品',
        ycsr:'10万',
        cb:'2万',
        zss:'2万',
        khs:'100万'
      },{
        tlcpxName:'轻工产品',
        ycsr:'10万',
        cb:'2万',
        zss:'2万',
        khs:'100万'
      },{
        tlcpxName:'电子电气',
        ycsr:'10万',
        cb:'2万',
        zss:'2万',
        khs:'100万'
      },{
        tlcpxName:'电子商务',
        ycsr:'10万',
        cb:'2万',
        zss:'2万',
        khs:'100万'
      },{
        tlcpxName:'文化艺术品鉴定',
        ycsr:'10万',
        cb:'2万',
        zss:'2万',
        khs:'100万'
      },{
        tlcpxName:'合计',
        ycsr:'50万',
        cb:'10万',
        zss:'10万',
        khs:'5万'
      }]
    },{
      olcpxName:'政府与机构',
      tcpxData:[{
        tlcpxName:'政府与国际贸易',
        ycsr:'24万',
        cb:'0万',
        zss:'0万',
        khs:'1000万'
      },{
        tlcpxName:'旧机电',
        ycsr:'24万',
        cb:'0万',
        zss:'0万',
        khs:'1000万'
      },{
        tlcpxName:'船舶舞毒蛾检查',
        ycsr:'24万',
        cb:'0万',
        zss:'0万',
        khs:'1000万'
      },{
        tlcpxName:'有害生物防制',
        ycsr:'24万',
        cb:'0万',
        zss:'0万',
        khs:'1000万'
      },{
        tlcpxName:'委托工厂检查',
        ycsr:'24万',
        cb:'0万',
        zss:'0万',
        khs:'1000万'
      },{
        tlcpxName:'公司与司法鉴定',
        ycsr:'24万',
        cb:'0万',
        zss:'0万',
        khs:'1000万'
      },{
        tlcpxName:'商务代理',
        ycsr:'24万',
        cb:'0万',
        zss:'0万',
        khs:'1000万'
      },{
        tlcpxName:'职业卫生及安全评价',
        ycsr:'24万',
        cb:'0万',
        zss:'0万',
        khs:'1000万'
      },{
        tlcpxName:'健康服务',
        ycsr:'24万',
        cb:'0万',
        zss:'0万',
        khs:'1000万'
      },{
        tlcpxName:'生态环境',
        ycsr:'24万',
        cb:'0万',
        zss:'0万',
        khs:'1000万'
      },{
        tlcpxName:'再生资源',
        ycsr:'24万',
        cb:'0万',
        zss:'0万',
        khs:'1000万'
      },{
        tlcpxName:'合计',
        ycsr:'264万',
        cb:'0万',
        zss:'0万',
        khs:'11000万'
      }]
    },{
      olcpxName:'认证服务与企业优化',
      tcpxData:[{
        tlcpxName:'体系和服务认证',
        ycsr:'24万',
        cb:'0万',
        zss:'0万',
        khs:'1000万'
      },{
        tlcpxName:'合计',
        ycsr:'264万',
        cb:'0万',
        zss:'0万',
        khs:'1000万'
      }]
    },{
      olcpxName:'其他',
      tcpxData:[{
        tlcpxName:'通用线',
        ycsr:'24万',
        cb:'0万',
        zss:'0万',
        khs:'1000万'
      },{
        tlcpxName:'合计',
        ycsr:'264万',
        cb:'0万',
        zss:'0万',
        khs:'1000万'
      }]
    });   
  },
  mounted(){
    // let left = $(".table_body .table_body_left"),
    //   lobj = left[left.length - 1],
    //   h = lobj.clientHeight;

    // $(lobj).attr('style','height:'+(h-1)+'px');

    // let right = $(".table_body .table_body_right"),
    //   robj = right[right.length - 1],
    //   rh = robj.clientHeight;

    // $(robj).attr('style','height:'+(rh+1)+'px');
  },
  methods: {}
}
</script>
<style lang='scss' scoped>
</style>
