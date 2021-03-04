<template>
  <div>
    <div class="zhuanpanBox" :style="{height:height+'px',width:height+'px'}">
      <div class="zhuanpanBoxUl" id="turnUl" :style="{height:height+'px',width:height+'px',transition:'transform ' + time / 1000 + 's ease',transform:'rotate(' + rotate + 'deg)'}">
        <img src="../../assets/luck.png" style="width:100%" alt="">
      </div>
      <div class="buttonBtn">
        <img src="../../assets/button.png" style="width:112px;height:135px" alt="">
      </div>
      <div class="buttonBtnText">
        <img class="buttonBtnTextImg" @click="startPlay" src="../../assets/go.png" style="width:67px;height:46px" alt="go">
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        list:[
          {id:1,title:'红包',angle:0},
          {id:2,title:'谢谢',angle:45},
          {id:3,title:'积分',angle:90},
          {id:4,title:'专车券',angle:135},
          {id:5,title:'帆布袋',angle:180},
          {id:6,title:'电子表',angle:225},
          {id:7,title:'台历',angle:270},
          {id:8,title:'肩枕',angle:315}
        ],
        pIndex: 0, // 中奖物品的下标
        rotNum:  0, // 旋转圈数基数
        time: 5000, // 旋转时间
        timer: null, // 定时器
        oTurntable: '', // 旋转圆盘背景图
        type: 0, // 0 图片 1 汉字,
        rotate:0
      }
    },
    components: {},
    props: {
      height:{
        type:[Number,String],
        default:0
      }
    },
    computed: {},
    methods: {
      async startPlay(){
        const a = {
          id:7,
          title:'8'
        };
        this.startBtn(a)
      },
      // 开始转动,通过奖项级别进行匹配:id
      async startBtn(val) {
        const self = this;
        self.list.forEach((i,d)=>{
          if(i.id == val.id){
            self.pIndex = d
          }
        });
        // 拿到相应的角度调旋转接口
        self.startrotate(self.list[self.pIndex].angle, () => {
          self.fulfillHandle(self.pIndex,self.list[self.pIndex].title);
        });
      },
      //开始旋转 angle角度  complete回调成功函数
      startrotate(angle, complete) {
        // 相应的角度 + 满圈 只是在原角度多转了几圈 360 * 6
        this.rotate = 2160 * (this.rotNum + 1) - 45*this.pIndex;
        clearTimeout(this.timer);
        // 设置5秒后停止旋转,处理接口返回的数据
        this.timer = setTimeout(() => {
          complete();
          this.rotNum++;
        }, this.time);
      },
      //得奖后的处理
      fulfillHandle(index,prizeName) {
        alert(index+'-'+prizeName)
      },
    },
    mounted() {

    }
  }
</script>
<style lang="scss" scoped>
  .buttonBtnTextImg{
    animation:shouzhi 1.2s linear infinite;
  }
  @keyframes shouzhi{
    0%{
      transform:scale(1);
    }
    50%{
      transform:scale(0.8);
    }
    100%{
      transform:scale(1);
    }
  }
  .zhuanpanBox{
    margin:0 auto;
    position: relative;
    .buttonBtn{
      position: absolute;
      z-index:12;
      top:50%;
      left:50%;
      margin-left:-56px;
      margin-top: -79.5px;
    }
    .buttonBtnText{
      position: absolute;
      z-index:14;
      top:50%;
      left:50%;
      margin-left:-33.5px;
      margin-top: -24px;
    }
    .zhuanpanBoxUl{
      position: relative;
      /*animation: rotate 1s linear infinite;*/
      @-webkit-keyframes rotate{from{-webkit-transform: rotate(0deg)}
        to{-webkit-transform: rotate(360deg)}
      }
      @-moz-keyframes rotate{from{-moz-transform: rotate(0deg)}
        to{-moz-transform: rotate(359deg)}
      }
      @-o-keyframes rotate{from{-o-transform: rotate(0deg)}
        to{-o-transform: rotate(359deg)}
      }
      @keyframes rotate{from{transform: rotate(0deg)}
        to{transform: rotate(359deg)}
      }
    }
  }
</style>
