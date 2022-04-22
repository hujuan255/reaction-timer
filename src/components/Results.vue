<template>
  <!-- 通过props接收父组件传递的成绩 -->
  <div class="results">你的反应时间为：{{ score }}毫秒</div>
  <!-- 排名 -->
  <p class="rank">{{ rank }}</p>
</template>
<script>
export default {
  name: "Results",
  // 通过props接收父组件传递的成绩
  props: ["score"],
  data() {
    return {
      // 初始化排名
      rank: null,
    };
  },
  mounted() {
    if (this.score < 250) {
      this.rank = "优秀！";
    } else if (this.score <= 450) {
      this.rank = "快速反应";
    } else {
      this.rank = "蜗牛速度";
    }
  },
};
</script>
<style scoped>
.rank {
  font-size: 20px;
  color: rgb(235, 155, 155);
  font-weight: 900;
}
</style>