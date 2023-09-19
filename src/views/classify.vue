<template>
    <div>
      <van-tabbar route active-color="#e64340">
      <van-tabbar-item icon="wap-home" to="/">首页</van-tabbar-item>
      <van-tabbar-item icon="card" to="/classify">菜单</van-tabbar-item>
      <van-tabbar-item icon="shopping-cart" to="/about">购物车</van-tabbar-item>
      <van-tabbar-item icon="manager" to="/my">我的</van-tabbar-item>
    </van-tabbar>

    <div class="head">分类</div>
    </div>
</template>

<script>
export default {
  data() {
     return {};
  },
  methods: {},
  computed: {},
  filters: {},
  watch: {},
 components: {}
};
</script>

<style lang="scss" scoped>
.head {
  width: 100%;
  padding: 10px 0;
  text-align: center;
}
</style>