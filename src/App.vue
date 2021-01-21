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
        发起post请求
      </div>
    </div>
    <hr/>
    <div>
      <h1>老虎机</h1>
      <div>
        <slotMachine/>
      </div>
    </div>
    <hr/>
    <div>
      <tiger></tiger>
    </div>
  </div>
</template>

<script>
import VuePicker from './components/picker/picker.vue';
import getAward from './components/get-award/get-award2'
import marquees from './components/marquees/marquees'
import eggNiu from './components/egg-niu/egg-niu'
import slotMachine from './components/slot-machine'
import tiger from './components/tiger'
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
    VuePicker,getAward,marquees,eggNiu,slotMachine,tiger
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
      let params = {name:'boonook',pwd:'123456'}
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
    }
  },
  mounted() {
    let data = this.getArrayDta();
    console.log(data)
  }
}
</script>

<style>
  #app{
    height:100vh;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
    background-color:rgba(0,0,0,0.3);
  }
</style>
