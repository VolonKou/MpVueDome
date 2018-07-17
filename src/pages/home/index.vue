<template>
  <div>
  <div >
    <ul class="Ul" style="margin-left: 5%">
      <li v-for="(item,key) in CutList" @click="GetItemid(item.id)" :key="key" class="LiItem">
        <div :class="{ItemBackgroundactive:active==item.id}" class="ItemBackground">
          <img :src="item.cate_pic" class="img"/>
        </div>
        <span style="font-size: 14px;margin-top: 5px">{{item.cate_name}}</span>

      </li>
    </ul>
  </div>
  <div style="margin-bottom: 30px">
    <ul>
      <li v-for="(item,key) in goodsList" @click="getcontainer(item.id)" :key="key" class="shopItem">
          <img :src="item.pic" style="width: 75px;height: 75px;margin-right: 15px"/>
        <div style="display: flex;flex-direction: column">
          <span>{{item.title}}</span>
          <span>{{item.sub_title}}</span>
          <p><span style="color: red;margin-right: 15px">￥{{item.price}}/盒</span><span style="text-decoration: line-through;color: #A7A7A7;">￥{{item.market_price}}</span></p>
        </div>

      </li>
    </ul>
  </div>
  </div>
</template>

<script>


export default {
  data() {
    return {
      CutList:[],
      goodsList:[],
      ItemId:27,
      active:0
    }
  },

  methods: {

    requestDate(){
      var _this=this

      var url="https://bpmeat.apicloudservices.com/api/cate?grade=2"

          wx.request({
            url: url, //仅为示例，并非真实的接口地址
            header: {
              'content-type': 'application/json' // 默认值
            },
            success: function(res) {
              _this.CutList=res.data.data
            }
          })


   this. GetItemid(_this.ItemId)

    },GetItemid(id){
      var _this=this
      _this.ItemId=id
      var defaultId=_this.ItemId
      _this.active=id





      var url="https://bpmeat.apicloudservices.com/api/goods?cate_id="+defaultId
      wx.request({
        url: url, //仅为示例，并非真实的接口地址
        header: {
          'content-type': 'application/json' // 默认值
        },
        success: function(res) {
          console.log(res.data.data)
          _this.goodsList=res.data.data
        }
      })

    },getcontainer(id){
      console.log(id)
    }

  },
  created(){
     this.requestDate()

  }
}

</script>

<style scoped>
  .Ul{
    display: flex;
    flex-wrap: wrap;
    width: 90%;
    justify-content: space-between;
    align-items:center;
    align-content: space-between;
  }
.LiItem{
  display: flex;
  flex-direction: column;
  width: 21%;
  margin-top: 20px;
  justify-content: center;
  align-items: center;
}
  .ItemBackground{
    width: 60px;
    height: 60px;
    border-radius: 30px;

    display: flex;
    justify-content: center;
    align-items: center;
  }
  .ItemBackgroundactive{
    background-color:#EFEFEF;
  }
.img{
  width: 50px;
  height: 50px;
}
  .shopItem{
    margin-top: 30px;
    display:flex;
    box-shadow: #CECECE 0px 0px 20px 4px;
    margin-right: 15px;
    margin-left: 15px;
    padding: 15px;
    border-radius: 10px 10px;
  }

</style>
