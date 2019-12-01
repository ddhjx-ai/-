// #mark 样式

<template>
  <div>
    <van-nav-bar title="电池异常报警" @click-left="onClickLeft" :border="false">
      <div slot="left" style="width:0.3rem;height:0.44rem;">
        <van-image :src="image" style="margin-top: 0.1rem; width:0.24rem; height:0.24rem ;" />
      </div>
    </van-nav-bar>

    <div class="subtitle">
      指定搜索范围
      <van-divider></van-divider>
    </div>
    <div class="btnFilterGroup">
      <van-button
        round
        type="default"
        :class="status==1?'btnFilterActive':'btnFilterdefault'"
        @click="listfilter(1)"
      >已处理</van-button>
      <van-button
        round
        type="default"
        :class="status==2?'btnFilterActive':'btnFilterdefault'"
        @click="listfilter(2)"
      >未处理</van-button>
    </div>

    <div style="width:100%;height:0.10rem ;background:#EDEDED ;margin-top:0.15rem"></div>

    <van-row
      type="flex"
      justify="center"
      v-for="(item ,index ) in dataList"
      :key="index"
      :class="item.status==1?'van-row_default':'van-row_active'"
    >
      <van-col span="8">{{item.reason}}</van-col>
      <van-col span="10">{{item.alarm_time}}</van-col>

      <van-col span="6">
        <span :class="item.status==1?'span_not':'span_ok'">{{item.status == 1 ?'故障' :'已处理'}}</span>
      </van-col>
    </van-row>
  </div>
</template>

<script>
export default {
  name: "BatteryError",
  data() {
    return {
      message: "",
      dataList: [],
      image: require("../../assets/ic_back_white.png"),
      scanImg: require("../../assets/mine_scan.png"),
      status: 1
    };
  },
  mounted() {
    console.log(111);

    // this.vinCode = this.$route.query.id;
    // console.log(this.vinCode);
    var parmas = {
      vin: this.vinCode
    };
    this.$post1("batteryError", parmas).then(res => {
      console.log(res);
      this.dataList = res.data;
    });
  },
  methods: {
    onClickLeft() {
      this.$router.go(-1); //返回上一层
    },
    btnClick(e) {
      console.log(e);
      // document.getElementsByClassName('btnFilterdefault')[0].style.background = 'red'
      // document.getElementsByClassName('van-button__text')[0].style.color = 'white'
      //fuck.css('background','red')
    },
    changeColor(status) {
      return status == 1 ? "dangerColor" : "successColor";
    },

    //---------------------------------------------
    //获取列表数据
    listfilter(status) {
      this.status = status;
    }
  }
};
</script>

<style lang="less"  scoped>
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

.subtitle {
  padding: 0 0.19rem;
  color: #666666;
  font-size: 0.13rem;
}

.van-button--normal {
  margin-right: 0.16rem;
  text-align: center;
}

.btnFilterGroup {
  padding: 0.1rem 0 0 0.19rem;
  .btnFilterActive {
    width: 0.81rem;
    height: 0.29rem;
    line-height: 0.29rem;
    padding: 0;
  }
  .van-button--normal {
    margin-right: 0.12rem;
  }
  .btnFilterdefault {
    height: 0.29rem;
    width: 0.7rem;
    padding: 0;
  }
  /deep/.van-button__text {
    justify-content: center;
  }
}

.van-divider {
  margin-top: 0;
  margin-bottom: 0.15rem;
}

/* .dangerColor {
  background: rgba(244, 15, 15, 0.3);
  color: rgba(244, 15, 15, 1);
}

.successColor {
  background: rgba(36, 187, 155, 0.3);
  color: rgba(36, 187, 155, 1);
} */

.active {
  font-family: PingFangSC-Medium;
  color: #24bb9b;
  letter-spacing: 0;
  text-align: center;
  line-height: 0.28rem;
  background: #e8f6f3;
  border-radius: 0.285rem;
}

// -------------------------------
.van-row_default {
  height: 0.55rem;
  padding-left: 0.19rem;
  line-height: 0.55rem;
  font-family: PingFangSC-Regular;
  color: #4a4a4a;
  .span_not {
    display: inline-block;
    line-height: 0.22rem;
    text-align: center;
    background: rgba(240, 117, 70, 0.1);
    border-radius: 0.02rem;
    font-size: 0.13rem;
    width: 0.56rem;
    height: 0.22rem;
    color: #f07546;
  }
}

.van-row_active {
  background: #f9f9f9;
  height: 0.55rem;
  padding-left: 0.19rem;
  line-height: 0.55rem;
  font-family: PingFangSC-Regular;
  color: #4a4a4a;
  .span_ok {
    font-size: 0.13rem;
    width: 0.56rem;
    height: 0.22rem;
    line-height: 0.22rem;
    display: inline-block;
    background: #e3f2ef;
    border-radius: 0.02rem;
    background-color: rgba(36, 187, 155, 0.1);
    color: #24bb9b;
    font-size: 0.13rem;
    text-align: center;
  }
}
</style>

 