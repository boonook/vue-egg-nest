<template>
  <div class="egg-niu">
      <div class="box">
          <div v-for="index of 11" :class="['qiu','qiu'+index]" :key="index"></div>
      </div>
      <div>
        开始
      </div>
  </div>
</template>

<script>
  export default {
    name: "egg-niu",
    props: {},
    components: {},

    computed: {
      imgUrl(){
        return function (index) {
          return require('./images/prize' + index + '.png')
        }
      }
    },
    data() {
      return {}
    },
    methods: {},
    mounted() {

    },
    watch: {},
    destroyed() {

    }
  }
</script>

<style lang="scss" rel="stylesheet/scss" scoped>
  .egg-niu {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    .box{
      margin-top:40px;
      width:300px;
      height:300px;
      border-radius:5px;
      border:1px solid orangered;
      position: relative;
    }
    .qiu{
      position: absolute;
      bottom:0;
      width:60px;
      height:60px;
      border-radius:60px;
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: center;
    }
    .qiu1{
      left:5px;
      bottom:0;
      animation:dialuodn 1s ease 0.1s forwards ;
    }
    .qiu1:after{content:"";
      position:absolute;
      left:0; bottom:0;
      width:60px;
      height:60px;
      background:url(./images/prize1.png) no-repeat;
      display:block;
      background-size:100%;
      animation:around1 1s ease forwards ;
    }
    .qiu2{
      left:60px;
      bottom:0;
      animation:dialuodn 1s ease 0.2s backwards;
    }
    .qiu3{
      left:120px;
      bottom:0;
      animation:dialuodn 1s ease 0.3s backwards;
    }
    .qiu4{
      left:180px;
      bottom:0;
      animation:dialuodn 1s ease 0.4s backwards
    }
    .qiu5{
      left:240px;
      bottom:0;
      animation:dialuodn 1s ease 0.5s backwards;
    }
    .qiu6{
      left:30px;
      bottom:40px;
      animation:dialuodn 1s ease 0.6s backwards;
    }
    .qiu7{
      left:90px;
      bottom:40px;
      animation:dialuodn 1s ease 0.7s backwards;
    }
    .qiu8{
      left:150px;
      bottom:40px;
      animation:dialuodn 1s ease 0.8s backwards;
    }
    .qiu9{
      left:210px;
      bottom:40px;
      animation:dialuodn 1s ease 0.9s backwards;
    }
    .qiu10{
      left:0;
      bottom:80px;
      animation:dialuodn 1s ease 1s backwards
    }
    .qiu11{
      left:60px;
      bottom:80px;
      animation:dialuodn 1s ease 1.1s backwards;
    }
    @keyframes dialuodn {
      0% {
        transform:translateY(-200%); opacity:0
      }
      5% {
        transform:translateY(-200%);
      }
      15% {
        transform:translateY(0);
      }
      30% {
        transform:translateY(-100%);
      }
      40% {

        transform:translateY(0%);
      }
      50% {
        transform:translateY(-60%);
      }
      70% {
        transform:translateY(0%);
      }
      80% {
        transform:translateY(-30%);
      }
      90% {
        transform:translateY(0%);
      }
      95% {
        transform:translateY(-14%);
      }
      97% {
        transform:translateY(0%);
      }
      99% {
        transform:translateY(-6%);
      }
      100% {
        transform:translateY(0);
        opacity: 1;
      }

    }
    @keyframes around1{
      0%{ transform:translate(0px,0px)  }
      22%{transform:translate(50px,-200px) }
      46%{transform:translate(240px,-100px) }
      80%{transform:translate(160px,6px) }
      100%{transform:translate(0px,0px) }
    }
  }
</style>
