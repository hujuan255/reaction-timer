<template>
  <h1>计时器</h1>
  <!-- 点击开始，调用start方法，游戏开始后开始按钮禁用 -->
  <button @click="start" :disabled="isplaying">开始游戏</button>
  <!-- 
      注入游戏组件(需引入，注册)，游戏开始才会让该组件显示，
      将延迟的时间(delay)通过props动态的传给子组件 Block.vue
      该父组件自定义事件end，在子组件通过this.$emit("end", this.reactionTimer),
      第一个参数为父组件中自定义事件的名称，第二个参数为子组件传递给父组件的参数(即反应时间)
  -->
  <Block v-if="isplaying" :delay="delay" @end="endGame"></Block>
  <!-- 
      注入结果组件(需引入，注册)，游戏结束后显示结果，
      如果有成绩才显示该组件
      将成绩(score)通过props动态的传给子组件Results.vue
   -->
  <Results v-if="isShowScore" :score="score"></Results>
</template>

<script>
// 引入组件
import Block from "./components/Block.vue";
import Results from "./components/Results.vue";
export default {
  name: "App",
  // 注册组件
  components: { Block, Results },
  data() {
    return {
      // 游戏开始前默认为false
      isplaying: false,
      //初始化延迟时间
      delay: null,
      // 初始化成绩(反应时间)
      score: 0,
      // 是否显示成绩
      isShowScore: false,
    };
  },
  methods: {
    //点击开始按钮调用该方法
    start() {
      //设置游戏随机时间为2~7秒
      this.delay = 2000 + Math.random() * 5000;
      //设置游戏开始
      this.isplaying = true;
      //游戏结束前不显示成绩
      this.isShowScore = false;
    },
    //自定义事件end调用的方法，参数为子组件的反应时间传给父组件的成绩
    endGame(reactionTime) {
      //设置成绩为子组件的反应时间
      this.score = reactionTime;
      //游戏结束，设置显示成绩
      this.isShowScore = true;
      //游戏结束，设置游戏不显示
      this.isplaying = false;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}
button {
  background: rgb(125, 185, 220);
  color: #fff;
  border: none;
  padding: 10px 20px;
  border-radius: 4px;
  font-size: 16px;
  /* 鼠标悬浮于连接上呈手的样式 */
  cursor: pointer;
  margin: 10px;
}
button[disabled] {
  /* 设置不透明度 */
  opacity: 0.2;
  /* 鼠标悬浮于连接上显示禁止的样式 */
  cursor: not-allowed;
}
</style>
