<template>
  <div id="app">
<!--    <div class="modal-box-top"></div>-->
<!--    <div class="modal-box">-->
<!--      <div class="modal-btn-box">-->
<!--        <div>-->
<!--          取消-->
<!--        </div>-->
<!--        <div class="modal-btn-box-right">-->
<!--          确定-->
<!--        </div>-->
<!--      </div>-->
<!--      <div class="modal-body">-->
<!--        <div class="modal-body-top"></div>-->
<!--        <div class="modal-body-footer"></div>-->
<!--        <ul >-->
<!--          <li>0&nbsp;&nbsp;0</li>-->
<!--          <li>0&nbsp;&nbsp;0</li>-->
<!--          <li>-->
<!--            湖北-->
<!--          </li>-->
<!--          <li>-->
<!--            湖南-->
<!--          </li>-->
<!--          <li>-->
<!--            广东-->
<!--          </li>-->
<!--          <li>-->
<!--            广西-->
<!--          </li>-->
<!--          <li>-->
<!--            山东-->
<!--          </li>-->
<!--          <li>-->
<!--            山西-->
<!--          </li>-->
<!--          <li>-->
<!--            陕西-->
<!--          </li>-->
<!--          <li>-->
<!--            北京-->
<!--          </li>-->
<!--          <li>-->
<!--            天津-->
<!--          </li>-->
<!--          <li>-->
<!--            重庆-->
<!--          </li>-->
<!--          <li>-->
<!--            上海-->
<!--          </li>-->
<!--          <li>-->
<!--            台湾-->
<!--          </li>-->
<!--          <li>-->
<!--            澳门-->
<!--          </li>-->
<!--          <li>-->
<!--            香港-->
<!--          </li>-->
<!--          <li>-->
<!--            辽宁-->
<!--          </li>-->
<!--          <li>-->
<!--            吉林-->
<!--          </li>-->
<!--          <li>-->
<!--            黑龙江-->
<!--          </li>-->
<!--          <li>&nbsp;&nbsp;</li>-->
<!--          <li>&nbsp;&nbsp;</li>-->
<!--        </ul>-->
<!--      </div>-->
<!--    </div>-->
    <div>
      <button @click="show">show picker</button>
      <VuePicker :data="pickData"
         :showToolbar="true"
         @cancel="cancel"
         :defaultIndex="[3,5,6,4]"
         @confirm="confirm"
         @change="onChange"
         :rowNumber="7"
         :visible.sync="pickerVisible"
      />
    </div>
    <div>
      <getAward :content-style="{width:'360px',height:'360px'}" :guuter="10"/>
    </div>
    <div>
      <marquees/>
    </div>
    <div>
      <egg-niu/>
    </div>
    <div>
      <div @click="_onRequest" style="background-color: orangered;height:48px;line-height:48px;text-align: center;border-radius:8px;margin:40px;color:#fff">
        egg发起post请求
      </div>
    </div>
    <div>
      <div @click="_onRequestNest" style="background-color: orangered;height:48px;line-height:48px;text-align: center;border-radius:8px;margin:40px;color:#fff">
        nestjs发起post请求
      </div>
    </div>
    <div>
      <div @click="_onRequestNestGet" style="background-color: orangered;height:48px;line-height:48px;text-align: center;border-radius:8px;margin:40px;color:#fff">
        nestjs发起get请求
      </div>
    </div>
    <div>
      <div @click="_onRequestNestDel" style="background-color: orangered;height:48px;line-height:48px;text-align: center;border-radius:8px;margin:40px;color:#fff">
        nestjs发起delete请求
      </div>
    </div>
    <hr/>
<!--    <div>-->
<!--      <h1>老虎机</h1>-->
<!--      <div>-->
<!--        <slotMachine/>-->
<!--      </div>-->
<!--    </div>-->
    <hr/>
    <div>
      <tiger></tiger>
    </div>
    <div>
      <h1>大转盘</h1>
      <rotate height="300"></rotate>
    </div>
    <div>
        <div class="niu">

        </div>
    </div>
  </div>
</template>

<script>
import VuePicker from './components/picker/picker.vue';
import getAward from './components/get-award/get-award2'
import marquees from './components/marquees/marquees'
import eggNiu from './components/egg-niu/egg-niu'
// import slotMachine from './components/slot-machine'
import tiger from './components/tiger';
import rotate from './components/dazhuanpan/rotate';
import moment from 'moment'
let tdata = [];
for (let i = 0; i < 20; i++) {
  tdata.push({
    label: '第' + i + '行',
    value: i
  })
}
export default {
  name: 'App',
  components: {
    VuePicker,getAward,marquees,eggNiu,tiger,rotate
  },
  data(){
    return{
      pickerVisible: false,
      pickData: [
        tdata,tdata,tdata,tdata
      ],
      result: '',
      list:[{name:'张三'},{name:'李四'},{name:'王五'}]
    }
  },
  methods:{
    show () {
      this.pickerVisible = true
    },
    cancel () {
      this.result = 'click cancel result: null'
    },
    confirm (res) {
      this.result = JSON.stringify(res)
    },
    onChange(res){
      console.log(res)
    },
    getArrayDta(){
      let length = this.list.length;
      let list = (new Array(20)).join('.').split('.');
      if(length < 1) {
        return this.list // 没有记录，就不用补充了
      }
      list = list.map((_, i) => this.list[i % length]);
      return list.concat(list.slice(0, 5)) // 凑齐25个数
        .map(s => `${ s.name }成功抢到`)
    },
    _onRequest(){
      let params = {name:'boonook',pwd:'123456'};
      fetch('http://127.0.0.1:7001/api/user/login',{
        method:"POST",   //请求方法
        body:JSON.stringify(params),   //请求体
        headers: {
          'Content-Type': 'application/json',
        }
      }).then(res=>{
        console.log(res);
      }).catch((error) => {
        alert(error)
      })
    },
    _onRequestNest(){
      let params = {username:'boonook',password:'12345'};
      fetch('http://127.0.0.1:3003/user/login',{
        method:"POST",   //请求方法
        body:JSON.stringify(params),   //请求体
        headers: {
          'Content-Type': 'application/json',
        }
      }).then(res=>{
        return  res.json();
      }).then(function(json) {
        console.log(json);
      });
    },
    _onRequestNestGet(){
      fetch('http://127.0.0.1:3003/article/list',{
        method:"GET",   //请求方法
      }).then(res=>{
        return  res.json();
      }).then(function(json) {
        console.log(json);
      });
    },
    _onRequestNestDel(){
      fetch('http://127.0.0.1:3003/cats/del/2',{
        method:"DELETE",   //请求方法
      }).then(res=>{
        return  res.json();
      }).then(function(json) {
        console.log(json);
      });
    },
    curry(fn){
      let length = fn.length;
      let args = [];
      return function curryFn(...curryArgs) {
        args = args.concat(curryArgs);
        if (args.length > length) {
          throw new Error('arguments length error')
        }
        if (args.length === length) {
          return fn(...args);
        }
        return curryFn;
      }
    },
    foo(a,b,c){
      return a + b + c
    },
    getDouYuList(){
      fetch('http://localhost:3003/httprequest/list',{
        method:"GET",   //请求方法
      }).then(res=>{
        return  res.json();
      }).then(function(json) {
        let times = moment(json.timeStamp).format('YYYY-MM-DD HH:mm:ss');
        console.log(times);
      });
    }
  },
  mounted() {
    let data = this.getArrayDta();
    console.log(data);
    (window.slotbydup=window.slotbydup || []).push({
      id: '3030834',
      container: 'ad_u123456'
    });
    //手动实现柯里化函数
    const curry_fn = this.curry(this.foo);
    console.log(curry_fn(1)(2)(3));
    if (window.WebSocket)
    {
      console.log("支持");
    }else
    {
      console.log("不支持");
    }
    let ws = new WebSocket("ws://localhost:3007");
    ws.onopen = function() {
      console.log("client：打开连接");
      let msg = {type:'test',id:'1453855454'};
      ws.send(JSON.stringify(msg));
      ws.send("client：hello，服务端");
    };
    ws.onmessage = function(e) {
      console.log("client：接收到服务端的消息 " + e.data);
      //   setTimeout(() => {
      //     ws.close();
      //   }, 5000);
    };
  },
}
</script>e.data

<style>
  #app{
    height:100vh;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
    background-color:rgba(0,0,0,0.3);
  }
  .niu{
    width:98.33px;
    height:103px;
    margin:0 auto;
    background-image: url("./assets/niu.jpg");
    background-size: auto 103px;
    animation: ox1 1s steps(6,start) 0ms infinite normal backwards;
  }
  @keyframes ox1 {
    0%{
      background-position:0 0;
    }
    100%{
      background-position:-590px 0;
    }
  }
</style>
