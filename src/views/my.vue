<template>
    <div>
      <van-tabbar route active-color="#e64340">
      <van-tabbar-item icon="wap-home" to="/">首页</van-tabbar-item>
      <van-tabbar-item icon="card" to="/classify">菜单</van-tabbar-item>
      <van-tabbar-item icon="shopping-cart" to="/about">购物车</van-tabbar-item>
      <van-tabbar-item icon="manager" to="/my">我的</van-tabbar-item>
    </van-tabbar>
    <div class="head">个人中心</div>

    <div class="con">
      <p>可用余额</p>
      <h3>0</h3>
    </div>
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
.con{
  width: 100%;
  text-align: center;
  padding: 20px 0;
  border-bottom: 1px solid #e8dec8;
  p{
    font-weight: 600;
  }
  h3{
    color: red;
  }
}
</style>