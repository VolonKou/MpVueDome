<template>
  <div>
    <ul class="Ul" style="margin-left: 5%">
      <li v-for="(item,key) in CutList" :key="key" class="LiItem">
        <div class="ItemBackground" style="">
          <img :src="item.cate_pic" class="img"/>
        </div>
        <span style="font-size: 14px;margin-top: 5px">{{item.cate_name}}</span>
      </li>
    </ul>
  </div>
</template>

<script>


export default {
  data() {
    return {
      CutList:[],
      goodsList:[]
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
              console.log(res.data.data)
              _this.CutList=res.data.data
            }
          })


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
li{
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
    background-color:#EFEFEF;
    display: flex;
    justify-content: center;
    align-items: center;

  }
.img{
  width: 50px;
  height: 50px;
}

</style>
