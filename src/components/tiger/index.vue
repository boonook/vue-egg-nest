<template>
  <div class="tiger">
    <div>
      <slot-machine
        :list="list1"
        :trigger="trigger"
        :currentIndex="currentIndex"
        :height="188"
        :width="87"
        @onComplete="onComplete">
      </slot-machine>
    </div>
    <div>
       <slot-machine
         :list="list2"
         :trigger="trigger"
         :currentIndex="currentIndex1"
         :height="188"
         :width="87"
         @onComplete="onComplete">
       </slot-machine>
    </div>
    <div>
      <slot-machine
        :list="list3"
        :trigger="trigger"
        :currentIndex="currentIndex2"
        :height="188"
        :width="87"
        @onComplete="onComplete">
      </slot-machine>
    </div>
    <div>
      <button @click="start">start</button>
    </div>
  </div>
</template>

<script>
  import SlotMachine from './SlotMachine';
  export default {
    name: "tiger",
    props: {},
    components: {SlotMachine},
    data() {
      return {
        list1: [
          {text: '1', color: '#668CFF',img: "https://cdn.rsscc.cn/ticket/images/cjhd_jp_miandan_0114@3x.png"},
          {text: '2', color: '#FF6666',img: "https://cdn.rsscc.cn/ticket/images/cjhd_jp_hongbao_0114@3x.png"},
          {text: '3', color: '#B366FF',img: "https://cdn.rsscc.cn/ticket/images/cjhd_jp_jifen_0114@3x.png"},
        ],
        list2: [
          {text: '4', color: '#668CFF',img:"https://cdn.rsscc.cn/ticket/images/cjhd_jp_miandan_0114@3x.png"},
          {text: '5', color: '#FF6666',img: "https://cdn.rsscc.cn/ticket/images/cjhd_jp_hongbao_0114@3x.png"},
          {text: '6', color: '#B366FF',img: "https://cdn.rsscc.cn/ticket/images/cjhd_jp_jifen_0114@3x.png"},
        ],
        list3: [
          {text: '7', color: '#668CFF',img:"https://cdn.rsscc.cn/ticket/images/cjhd_jp_miandan_0114@3x.png"},
          {text: '8', color: '#FF6666',img:"https://cdn.rsscc.cn/ticket/images/cjhd_jp_hongbao_0114@3x.png"},
          {text: '9', color: '#B366FF',img:"https://cdn.rsscc.cn/ticket/images/cjhd_jp_jifen_0114@3x.png"},
        ],
        currentIndex:1,
        currentIndex1:2,
        currentIndex2:0,
        trigger: null,
      }
    },
    methods: {
      start() { // Trigger to let the machine start
        this.trigger = new Date();
      },
      onComplete(data) { // Run complete callback
        console.log(data);
      }
    },
    mounted() {

    },
    watch: {},
    destroyed() {

    }
  }
</script>

<style lang="scss" rel="stylesheet/scss" scoped>
  .tiger {
    display: flex;
    flex-direction: row;
  }
</style>
