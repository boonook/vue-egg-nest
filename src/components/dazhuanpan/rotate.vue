<template>
  <div>
    <div class="zhuanpanBox">
      <ul class="zhuanpanBoxUl" id="turnUl">
        <li v-for="(item,index) in list" :key="index">{{item.title}}</li>
      </ul>
      <div class="startBtn">
        <img @click="startPlay" src="../../assets/o_go.jpg" alt="">
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        list:[
          {id:1,title:'1-1',angle:0},
          {id:2,title:'2',angle:45},
          {id:3,title:'3',angle:90},
          {id:4,title:'4',angle:135},
          {id:5,title:'5',angle:180},
          {id:6,title:'6',angle:225},
          {id:7,title:'7',angle:270},
          {id:8,title:'8',angle:315}
        ],
        pIndex: 0, // 中奖物品的下标
        rotNum:  0, // 旋转圈数基数
        time: 5000, // 旋转时间
        timer: null, // 定时器
        oTurntable: '', // 旋转圆盘背景图
        type: 0, // 0 图片 1 汉字
      }
    },
    components: {},
    props: {},
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
        let rotate = 2160 * (this.rotNum + 1) - 45*this.pIndex;
        this.oTurntable.style.webkitTransform = 'rotate(' + rotate + 'deg)';
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
      this.oTurntable = document.querySelector('#turnUl');
      // 过度中属性用时5s
      this.oTurntable.style.webkitTransition = 'transform ' + this.time / 1000 + 's ease';
    }
  }
</script>
<style lang="scss" scoped>
  .zhuanpanBox{
    width:300px;
    height:300px;
    background-color:orangered;
    margin:0 auto;
    margin-top:40px;
    border-radius:150px;
    position: relative;
    .startBtn{
      position: absolute;
      width:50px;
      height:50px;
      z-index:20;
      top:50%;
      left:50%;
      margin-left:-25px;
      margin-top:-25px;
      img{
        width:100%;
      }
    }
    li{
      width:40px;
      height:40px;
      background-color: green;
      border-radius:20px;
      text-align: center;
      line-height:40px;
    }
    .zhuanpanBoxUl{
      width:300px;
      height:300px;
      border-radius:150px;
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
    li:nth-child(1){
      position: absolute;
      z-index:9;
      top:0;
      left:50%;
      margin-top: 2px;
      margin-left:-20px;
    }
    li:nth-child(2){
      position: absolute;
      z-index:9;
      top: 15%;
      left: 75%;
    }
    li:nth-child(3){
      position: absolute;
      z-index:9;
      top:50%;
      left:100%;
      margin-top:-20px;
      margin-left:-40px;
    }
    li:nth-child(4){
      position: absolute;
      z-index:9;
      top: 74%;
      left: 74%;
    }
    li:nth-child(5){
      position: absolute;
      z-index:9;
      bottom:0;
      left:50%;
      margin-left:-20px;
    }
    li:nth-child(6){
      position: absolute;
      z-index:9;
      top: 75%;
      left: 14%;
    }
    li:nth-child(7){
      position: absolute;
      z-index:9;
      left:0;
      top:50%;
      margin-top:-20px;
    }
    li:nth-child(8){
      position: absolute;
      z-index:9;
      top: 15%;
      left: 11%;
    }
  }
</style>
