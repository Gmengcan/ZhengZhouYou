<template>
  <div>
    <van-tabbar route active-color="#e64340">
      <van-tabbar-item icon="wap-home" to="/">首页</van-tabbar-item>
      <van-tabbar-item icon="card" to="/classify">菜单</van-tabbar-item>
      <van-tabbar-item icon="shopping-cart" to="/about">购物车</van-tabbar-item>
      <van-tabbar-item icon="manager" to="/my">我的</van-tabbar-item>
    </van-tabbar>

    <div class="head">未来好面</div>

    <van-swipe class="my-swipe" :autoplay="3000" indicator-color="white">
      <van-swipe-item v-for="item in banner" :key="item.id">
        <img :src="item.picUrl" alt="">
      </van-swipe-item>
    </van-swipe>

    <div class="box" v-for="items in item" :key="item.id">
      <div class="bot">{{ items.name }}</div>  
      <div class="box1">
        <div class="left">
          <van-icon name="location-o" />
          {{ items.address }}
        </div>
        <div class="right">
          地图>
        </div>
      </div>
      <div class="box1">
        <div class="left">
          <van-icon name="underway-o" />
          营业时间
        </div>
        <div class="right">
          {{ items.openingHours }}
        </div>
      </div>
      <div class="box1">
        <div class="left">
          <van-icon name="phone-o" />
          联系电话
        </div>
        <div class="right">
          {{items.linkPhone}}
        </div>
      </div>
    </div>

    <h2>店家推荐</h2>

    <div class="list">
      <my-list class="item" v-for="item in list" :key="item.id" :item="item" @todetail="todetail"></my-list>
    </div>
  </div>
</template>

<script>
import myList from '../components/myList.vue'
export default {
  data() {
    return {
      banner: [],
      item: [],
      list:[]
    };
  },
  methods: {
    //录播图
    getbanner() {
      this.$axios.get('https://api.it120.cc/noodles/banner/list').then((res) => {
        console.log(res,'banner');
        this.banner = res.data.data
      })
    },
    //店铺信息
    getItem() {
      this.$axios.get('https://api.it120.cc/noodles/shop/subshop/list').then((res) => {
        console.log(res,'item');
        this.item = res.data.data
      })
    },
    //list数据
    getlist(){
      this.$axios.post('https://api.it120.cc/noodles/shop/goods/list?recommendStatus=1').then((res)=>{
        console.log(res,'list');
        this.list = res.data.data
      })
    },
    //跳转详情
    todetail(id){
      this.$router.push({path:'/detail',query:{id:id}})
    }
  },
  computed: {},
  filters: {},
  watch: {},
  components: {
    myList
  },
  created() {
    this.getbanner()
    this.getItem()
    this.getlist()
  }
};
</script>

<style lang="scss" scoped>
.head {
  width: 100%;
  padding: 10px 0;
  text-align: center;
}

.van-swipe {
  img {
    width: 100%;
    height: 200px;
  }
}
.box{
  width: 100%;
  .bot{
    padding:10px;
    color: #8d867d;
    border-bottom: 1px solid #d6d2ca;
  }
  .box1{
    width: 100%;
    display: flex;
    justify-content: space-between;
    padding: 8px;
    box-sizing: border-box;
    border-bottom: 1px solid #d6d2ca;
    .right{
      color: #96938d;

    }
  }
}
h2{
  width: 100%;
  font-weight: 540;
  text-align: center;
}
.list{
  width: 100%;
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  margin-bottom: 50px;
  .item{
    width: 48%;
    margin-bottom: 17px;
  }
}
</style>