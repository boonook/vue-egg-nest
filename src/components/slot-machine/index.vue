<template>
      <div :class="{ contain: !loading }">
        <div id="page-all" class="contain">
          <!-- 抽奖机 -->
          <homePageSlotMachine
            :lotteryItems="lotteryItems"
            :btnId="btnId"
            :isRoating="isRoating"
            :award1="award1"
            :award2="award2"
            :award3="award3"
          ></homePageSlotMachine>
          <!-- 按钮 -->
          <div class="click-btn-box">
            <div class="click-btn" @click="clickBtn">
              <img src="./images/btn0.png" alt=""/>
            </div>
          </div>
        </div>
      </div>
</template>
<script>
// 组件
import homePageSlotMachine from "./module/homePageSlotMachine";
export default {
  name: "springTravel",
  data() {
    return {
      loading: false,
      btnId: 0, // 开始抽奖0  抽奖ing1 分享好友2 明天再来3 再抽一次4 第二次抽奖ing5
      isRoating: false,
      lotteryTitles: [

      ], //中奖名单
      lotteryItems: [
        {img: "https://cdn.rsscc.cn/ticket/images/cjhd_jp_miandan_0114@3x.png",
          itemId: "2_extract_free",
          name: "0元抽免单",
          type: "extract_free"
        },{
          img: "https://cdn.rsscc.cn/ticket/images/cjhd_jp_hongbao_0114@3x.png",
          itemId: "3_coupon",
          name: "20元返现红包",
          type: "coupon"
        },{
          img: "https://cdn.rsscc.cn/ticket/images/cjhd_jp_jifen_0114@3x.png",
          itemId: "4_integral",
          name: "20积分",
          type: "integral",
        }
      ], //奖品列表
      share: null, //分享次数
      lastTimes:100, //抽奖次数
      awardResults: [
        {
          img: "https://cdn.rsscc.cn/ticket/images/cjhd_jp_jifen_0114@3x.png",
        itemId: "4_integral",
        name: "20积分",
        type: "integral"
      },{
        img: "https://cdn.rsscc.cn/ticket/images/cjhd_jp_jifen_0114@3x.png",
        itemId: "4_integral",
        name: "20积分",
        type: "integral",
      },{
        img: "https://cdn.rsscc.cn/ticket/images/cjhd_jp_hongbao_0114@3x.png",
        itemId: "3_coupon",
        name: "20元返现红包",
        type: "coupon"
      }], //抽奖结果
      award1: {
        img: "https://cdn.rsscc.cn/ticket/images/cjhd_jp_jifen_0114@3x.png",
        itemId: "4_integral",
        name: "20积分",
        type: "integral"
      },
      award2: {
        img: "https://cdn.rsscc.cn/ticket/images/cjhd_jp_jifen_0114@3x.png",
        itemId: "4_integral",
        name: "20积分",
        type: "integral",
      },
      award3: {
        img: "https://cdn.rsscc.cn/ticket/images/cjhd_jp_hongbao_0114@3x.png",
        itemId: "3_coupon",
        name: "20元返现红包",
        type: "coupon"
      },
      status: 0,
    };
  },
  methods: {
    clickBtn() {
     this.btnId = 1;
     this.isRoating = true;
    }
  },
  components: {
    homePageSlotMachine,
  },
};
</script>
<style lang="scss" scoped>
.contain {
  height: 495px;
  background-size: 100% auto;
  position: relative;
  overflow: hidden;
  background-color: #fdca0b;
  #page-all {
    overflow: hidden;
    position: relative;
    .click-btn-box {
      position: absolute;
      top: 357px;
      left: 50%;
      transform: translateX(-50%);
      width: 165px;
      height: 57px;
      margin: 0 auto 40px;
      overflow: hidden;
      .click-btn {
        width: 100%;
        height: 100%;
        overflow: hidden;

        img {
          width: 100%;
          height: 100%;
        }
      }
    }
  }
}
</style>
