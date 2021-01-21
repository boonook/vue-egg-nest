<template>
  <div class="get-award" :style="{backgroundColor:'aquamarine',...contentStyle}">
    <div id="rotary-table" style="width:350px">
      <div class="award" v-for="(award,index) in awards" :key="index" :class="['award'+index]">
        <div style="margin: 10px;
            margin-right:0;
            background-color: orangered;
            width: calc(100% - 10px);
            height: calc(100% - 10px);
            margin-bottom:0;
            "
            :class="[{'active': index==current}]"
        >
          {{award.name}}
        </div>
      </div>
      <div id="start-btn" @click="start">
        <div style="margin: 10px;
            margin-right:0;
            background-color:coral;
             width: calc(100% - 10px);
            height: calc(100% - 10px);
             margin-bottom:0;"
        >
          开始
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "get-award",
    props: {
      contentStyle:{
        type:Object,
        default:function () {
          return {}
        }
      },
      guuter:{
        type:Number,
        default:0
      }
    },
    components: {},
    data() {
      return {
        current: 0,
        awards: [  // 奖品数组
          { id: 1, name: '空' },
          { id: 2, name: '眼镜' },
          { id: 3, name: '包' },
          { id: 4, name: '笨驴' },
          { id: 5, name: '书' },
          { id: 6, name: '手链' },
          { id: 7, name: '美女' },
          { id: 8, name: 'iphone' }
        ],
        speed: 200,   // 速度
        diff: 15,   // 速度增加的值
        award: {},   // 抽中的奖品
        time: 0   // 记录开始抽奖时的时间
      };
    },
    methods: {
      start(){
        // 开始抽奖
        this.drawAward();
        this.time = Date.now();
        this.speed = 200;
        this.diff = 15;
      },
      drawAward(){
        // 请求接口, 这里我就模拟请求后的数据(请求时间为2s)
        setTimeout( () => {
          this.award = {
            id: '2',
            name: '眼睛',
          };
        }, 2000 );
        this.move();
      },
      move(){
        window.timeout = setTimeout( () => {
          this.current++;
          if ( this.current > 7 ) {
            this.current = 0;
          }

          // 若抽中的奖品id存在，则开始减速转动
          if ( this.award.id && ( Date.now() - this.time ) / 1000 > 2 ) {
            this.speed += this.diff;   // 转动减速

            // 若转动时间超过4秒，并且奖品id等于小格子的奖品id，则停下来！
            if ( ( Date.now() - this.time ) / 1000 > 4 && this.award.id == this.awards[ this.current ].id ) {
              clearTimeout( window.timeout );
              setTimeout( () => {
                alert( this.award.name );
              }, 0 );
              return;
            }

            // 若抽中的奖品不存在，则加速转动
          } else {
            this.speed -= this.diff;   // 转动加速
          }

          this.move();
        }, this.speed );
      }
    },
    mounted() {

    },
    watch: {},
    destroyed() {

    }
  }
</script>
<style rel="stylesheet/scss" lang="scss">
  * {
    margin: 0;
    padding: 0;
    list-style: none;
    outline: none;
  }
  #rotary-table {
    width: 350px;
    height: 350px;
    position: relative;
    background-color: aquamarine;
  }
  .award {
    width:33.33333%;
    height:33.33333%;
    text-align: center;
    float: left;
    position: absolute;
    overflow: hidden;
    background-color: aquamarine;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
 .active {
    background-color: darkgoldenrod!important;
  }
 .award0 {
    top:0;
    left:0;
  }
  .award1 {
    top:0;
    left:33.33333%;
  }
  .award2 {
    top:0;
    right:0;
  }
  .award3 {
    top:33.33333%;
    right:0;
  }
 .award4 {
    bottom:0;
    right:0;
  }
   .award5 {
     bottom:0;
     right:33.33333%;
  }
 .award6 {
    bottom:0;
    left:0;
  }
  .award7 {
    top:33.33333%;
    left:0;
  }
  #start-btn {
    position: absolute;
    top:33.33333%;
    left:33.33333%;
    width:33.33333%;
    height:33.33333%;
    text-align: center;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
</style>
