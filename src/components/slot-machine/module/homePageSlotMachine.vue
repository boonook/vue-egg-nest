<template>
  <div class="homepage-slotmachine">
    <img src="../images/up_shadow.png" alt="" class="up-shadow" />
    <img src="../images/down_shadow.png" alt="" class="down-shadow" />
    <div class="awards-box">
      <div class="redpaper" v-if="!isRoating || btnId === 4">
        <img src="../images/redpaper.png" />
      </div>
      <div
        :class="[isRoating ? 'rotating1' : '']"
        v-if="btnId == 0 || btnId == 1 || btnId == 5"
      >
        <img :src="i1" alt="" v-for="(i1, k1) in box1" :key="k1" />
      </div>
      <div v-if="btnId === 2 || btnId == 3">
        <img :src="award1.img" />
      </div>
    </div>
    <div class="awards-box">
      <div class="redpaper" v-if="!isRoating || btnId === 4">
        <img src="../images/redpaper.png" />
      </div>
      <div
        :class="[isRoating ? 'rotating2' : '']"
        v-if="btnId == 0 || btnId == 1 || btnId == 5"
      >
        <img :src="i2" alt="" v-for="(i2, k2) in box2" :key="k2" />
      </div>
      <div v-if="btnId === 2 || btnId == 3">
        <img :src="award2.img" />
      </div>
    </div>
    <div class="awards-box">
      <div class="redpaper" v-if="!isRoating || btnId === 4">
        <img src="../images/redpaper.png" />
      </div>
      <div
        :class="[isRoating ? 'rotating3' : '']"
        v-if="btnId == 0 || btnId == 1 || btnId == 5"
      >
        <img :src="i3" alt="" v-for="(i3, k3) in box3" :key="k3" />
      </div>
      <div v-if="btnId === 2 || btnId == 3">
        <img :src="award3.img" />
      </div>
    </div>
  </div>
</template>
<script>
import prize1 from "../images/extract_free2.png";
import prize2 from "../images/integral2.png";
import prize3 from "../images/hbgj_member2.png";
import prize4 from "../images/coupon2.png";
export default {
  data() {
    return {
      box1: [
        prize1,
        prize2,
        prize3,
        prize4,
        prize1,
        prize2,
        prize4,
        prize1,
        prize2,
      ],
      box2: [
        prize2,
        prize3,
        prize1,
        prize4,
        prize1,
        prize2,
        prize4,
        prize2,
        prize1,
      ],
      box3: [
        prize4,
        prize4,
        prize1,
        prize2,
        prize2,
        prize1,
        prize3,
        prize3,
        prize4,
      ],
    };
  },
  props: {
    btnId: {
      type: Number,
      default: 0,
    },
    isRoating: {
      type: Boolean,
      dafault: false,
    },
    lotteryItems: {
      type: Array,
    },
    award1: {
      type: Object,
    },
    award2: {
      type: Object,
    },
    award3: {
      type: Object,
    },
  },
  components: {},
  methods: {},
};
</script>
<style lang="scss" scoped>
.homepage-slotmachine {
  position: relative;
  margin-top: 230px;
  margin-left: 45px;
  width: 286px;
  height: 100px;
  padding: 4px 7px;
  box-sizing: border-box;
  display: flex;
  justify-content: space-between;
  align-items: center;
  .up-shadow,
  .down-shadow {
    display: inline-block;
    width: 100%;
    position: absolute;
    left: 0;
    z-index: 1;
  }
  .up-shadow {
    top: 0;
  }
  .down-shadow {
    bottom: 0;
  }
  .awards-box {
    position: relative;
    width: 87px;
    height: 94px;
    overflow: hidden;
    img {
      width: 100%;
      height: 100%;
    }
    .rotating1 {
      position: absolute;
      animation: goRoate 4s 1;
    }
    .rotating2 {
      position: absolute;
      animation: goRoate 6s 1;
    }
    .rotating3 {
      position: absolute;
      animation: goRoate 8s 1;
    }
  }
}
@keyframes goRoate {
  from {
    transform: translateY(0%);
  }
  to {
    transform: translateY(-90%);
  }
}
</style>
