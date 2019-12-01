// #mark  添加 扫码scan() 函数；searchBtnClick() 函数；  样式；

<template>
  <div>
    <van-nav-bar title="回收查询" @click-left="onClickLeft" :border="false">
      <div slot="left" style="width:0.3rem;height:0.44rem;">
        <van-image :src="image" style="margin-top: 0.1rem; width:0.24rem; height:0.24rem ;" />
      </div>
    </van-nav-bar>

    <div
      style="width:100%;height:0.61rem;background:#24BB9B;display:flex;flex-direction:row;align-items:center;"
    >
      <div class="inputView">
        <input class="input" placeholder="请输入或扫描电池包码" />
      </div>
      <img :src="scanImg" style="width: 0.23rem;margin-left: -0.4rem; z-index:1000" @click="scan" />
      <div class="cancleBtn" @click="searchBtnClick">搜索</div>
    </div>

    <div
      style="background:#f8f8f8;padding:0 0.19rem;font-family: PingFangSC-Medium;font-size: 0.14rem;color: #333333;height:0.49rem;line-height:0.49rem;"
    > <p style="margin:0;height:100%;width:100%;border-bottom: 1px solid #E8E8E8;box-sizing:border-box">搜索历史</p></div>

    <!-- 居中 -->
    <div v-for="item in 6" :key="item" style="height:0.55rem;padding:0.15rem 0.19rem;box-sizing:border-box">
      <van-row >
        <van-col span="20">LFV219DK32939234</van-col>
      </van-row>
    </div>
  </div>
</template>

<script>
export default {
  name: "BackSearch",

  data() {
    return {
      message: "",
      image: require("../../assets/ic_back_white.png"),
      scanImg: require("../../assets/mine_scan.png"),

      historyData: ""
    };
  },

  mounted(){
    // ---------------------------------------电池包码
    var data = localStorage.getItem("batteryCode");
    var dataObj = JSON.parse(data);
    if (dataObj) this.historyData = dataObj.reverse();
  },

  methods: {
    onClickLeft() {
      this.$router.go(-1); //返回上一层
    },

    // 扫码*************************************
    scan() {
      console.log(111);
      triggerNative("saoyisao", "", (val) => {
        console.log(res)
      });
    },
    // 搜索*************************************
    searchBtnClick() {
      console.log(13213)
      if (!this.message) {
        this.$toast.fail("请输入电池包码");
        return;
      }
      var data = localStorage.getItem("batteryCode");
      var dataObj = JSON.parse(data);
      if (dataObj) {
        if (dataObj.length > 7) {
          var item = dataObj.splice(1, 8);
          item.push(this.message);
          localStorage.setItem("batteryCode", JSON.stringify(item));
        } else {
          dataObj.push(this.message);
          localStorage.setItem("batteryCode", JSON.stringify(dataObj));
        }
      } else {
        dataObj = [];
        dataObj.push(this.message);
        localStorage.setItem("batteryCode", JSON.stringify(dataObj));
      }

      // this.$router.push({
      //   path: "/CarDetail",
      //   query: { id: this.message }
      // });
    }
  }
  // beforeRouteLeave(to, from, next) {
  //      // 设置下一个路由的 meta
  //      console.log('123455x')
  //     // to.meta.keepAlive = true;  // B 跳转到 A 时，让 A 缓存，即不刷新
  //     // next();
  // }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.van-nav-bar {
  background: #24bb9b;
}
.van-nav-bar .van-icon {
  color: white;
}
.van-nav-bar__title {
  color: white;
  font-size: 0.19rem;
}

.van-cell__value {
  color: #333333;
}

.inputView {
  background: #27c6a5;
  border-radius: 0.36rem;
  line-height: 0.36rem;
  width: 2.94rem;
  height: 0.36rem;
  margin-left: 0.19rem;
}
.input {
  margin-left: 0.2rem;
  background: #27c6a5;
  border: none;
  height: 80%;
  width: 60%;
  margin-top: 0;
}

::-webkit-input-placeholder {
  color: #D5FFF6;
  font-size: 0.15rem;
}
.cancleBtn {
  font-family: PingFangSC-Regular;
  font-size: 0.14rem;
  color: #ffffff;
  line-height: 0.3rem;
  width: 0.8rem;
  height: 0.3rem;
  position: absolute;
  right: 0.19rem;
  text-align: right;
}
.van-col {
  width: 100%;
  box-sizing: border-box;
  background: #f5f8f8;
  border-radius: 0.04rem;
  text-align: left;
  height: 0.3rem;
  line-height: 0.3rem;
  font-size: 0.14rem;
  color: #666;
  text-indent: 0.11rem;
}
</style>

