<template>
  <!-- 延迟时间加载完显示该模块，点击自身Dom停止游戏 -->
  <div v-show="isShowBlock" class="block" @click="stopTimer">Click me</div>
</template>
<script>
export default {
  name: "Block",
  // 通过props接受父组件传递的延迟时间
  props: ["delay"],
  data() {
    return {
      // 游戏开始前默认为false
      isShowBlock: false,
      //初始化间隔时间
      timer: null,
      //初始化反应时间
      reactionTimer: 0,
    };
  },
  mounted() {
    //console.log("组件加载完成");
    //游戏开始后，调用该延迟方法
    setTimeout(() => {
      //延迟时间到，该模块显示
      this.isShowBlock = true;
      //调用游戏开始计时
      this.startTimer();
      //延迟时间，通过props从父组件中获得
    }, this.delay);
  },
  methods: {
    //开始计时
    startTimer() {
      //每10毫秒重新累计一次反应时间
      this.timer = setInterval(() => {
        this.reactionTimer += 10;
      }, 10);
    },
    //停止计时
    stopTimer() {
      //清除计时器
      clearInterval(this.timer);
      //console.log(this.reactionTimer);
      //将反应时间通过自定义事件传递给父组件
      this.$emit("end", this.reactionTimer);
    },
  },
  //当组件中的对象、数据发生变化时，会自动调用该方法
  // updated() {
  //   console.log("组件更新完成");
  // },
};
</script>
<style scoped>
.block {
  width: 400px;
  height: 300px;
  background-color: rgb(125, 185, 220);
  border-radius: 20px;
  padding: 10px 20px;
  margin: 100px auto;
  color: #fff;
  text-align: center;
  line-height: 300px;
}
</style>