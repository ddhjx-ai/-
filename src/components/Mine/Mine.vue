<template>
  <div style="width:100%;background:white;height:100vh;">
    <div class="top_view">
      <van-image :src="image" width="0.58rem" height="0.58rem" style="margin-left: 0.15rem;" round />
      <div style=" margin-left: 0.1rem;">
        <div style="display:flex;flex-direction: row ;color:rgba(255, 255, 255, 1) ;font-size:18px">
          {{userName}}
          <div style="color:rgba(255, 255, 255, 1);font-size:12px;line-height: 26px;"> </div>
        </div>
        <div
          style="font-size: 9px;color: rgba(255, 255, 255, 1);margin-top:0.05rem"
        >{{userPhone}}</div>
      </div>

      <!-- <div  class= 'rightBtn' > </div> -->
    </div>

    <div
      style="width: 100%; height: 0.2rem; background: white;margin-top: -0.3rem;border-top-left-radius: 0.2rem;border-top-right-radius: 0.2rem;"
    ></div>
    <van-cell
      :title="item"
      :icon="imgList[index]"
      is-link
      :border="false"
      v-for="(item, index) in dataList"
      :key="item"
      @click="cellClick(index)"
    />

    <!-- <van-field /> -->
    <!-- <div style="width=100% ;height:400px;background:white"></div> -->
  </div>
</template>

<script>
export default {
  name: "Mine",
  data() {
    return {
       userName:'',
      userPhone:'' ,
      dataList: [
        "车辆信息绑定",
        "车辆信息查询",
        "电池运行状态监控",
        "电池异常报警",
        "投诉与建议"
      ],
      image: require("../../assets/logo.png"),
      imgList: [
        require("../../assets/mine_icon1.png"),
        require("../../assets/mine_icon2.png"),
        require("../../assets/mine_icon3.png"),
        require("../../assets/mine_icon4.png"),
        require("../../assets/mine_icon7.png")
      ]
    };
  },
  mounted(){
    
  this.userName = sessionStorage.getItem('userName'),
  this.userPhone = sessionStorage.getItem('userPhone') 
          
 },
  methods: {
    cellClick(index) {
      switch (index) {
        case 0:
          {
            this.$router.push({
              path: "/BindCarInfo"
            });
          }

          break;
        case 1:
          {
            this.$router.push({
              path: "/CarBindingList",
              query: { id: "1234" }
            });
          }
          break;

        case 2:
          {
            this.$router.push({
              path: "/BatteryOperationStatus"
            });
          }
          break;
        case 3:
          {
            this.$router.push({
              path: "/BatteryError"
            });
          }
          break;
        //  case 4:
        //       {
        //    this.$router.push({
        //     path:'/CarRepairInfo'
        //   })
        //       }
        //       break;

        //  case 4:
        //       {
        //    this.$router.push({
        //     path:'/RecoveryEvaluation'
        //   })
        //    }
        //       break;

        case 4:
          {
            this.$router.push({
              path: "/Ajust",
              query: { id: "1234" }
            });
          }
          break;
        default:
          break;
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.top_view {
  width: 100%;
  height: 2.2rem;
  display: flex;
  flex-direction: row;
  align-items: center;
  /* margin-bottom: 0.2rem; */
  /* justify-content: center ; */
  background: linear-gradient(-53deg, #24bb9b 0%, #29cdaa 95%);
}
.rightBtn {
  color: rgba(255, 255, 255, 1);
  font-size: 12px;
  border: 1px solid white;
  /* padding-left: 0.1rem; */
  /* padding-right: 0.1rem; */
  /* padding-top: 0.05rem; */
  /* padding-bottom: 0.05rem; */
  border-radius: 0.2rem;
  height: 0.25rem;
  width: 0.7rem;
  text-align: center;
  line-height: 0.25rem;
  margin-left: 0.08rem;
}
</style>
