<template>
  <div>
    <van-tabbar route active-color="#e64340">
      <van-tabbar-item icon="wap-home" to="/">首页</van-tabbar-item>
      <van-tabbar-item icon="card" to="/classify">菜单</van-tabbar-item>
      <van-tabbar-item icon="shopping-cart" to="/about">购物车</van-tabbar-item>
      <van-tabbar-item icon="manager" to="/my">我的</van-tabbar-item>
    </van-tabbar>
    <div class="head">购物车</div>
    <div class="con" v-show="shop.length != 0">
      <span>您选购的商品</span>
      <span class="s1" @click="bj">编辑</span>
    </div>

    <shop-list v-for="item in shop" :key="item.id">
      <div class="shop">
        <van-checkbox v-model="item.flag" @click="checkedFn"></van-checkbox>
        <van-swipe-cell class="itm">
        <van-card :price="item.minPrice"  :title="item.name" class="goods-card"
          :thumb="item.pic">
          <template #footer>
            <van-stepper v-model="item.num"/>
          </template>
        </van-card>
        <template #right>
          <van-button square text="删除" type="danger" class="delete-button" @click="del(item.id)" />
        </template>
      </van-swipe-cell>
    </div>
    </shop-list>
    <shop-foot>
      <div class="foot" v-show="shop.length != 0">
            <div class="left">
            <van-checkbox v-model="checked" @click="changeAll">全选</van-checkbox>
            </div>
            <div class="right">
                <span class="s1">合计:￥{{ sum }}</span>
                <button @click="remove">{{ status== true?'删除选中':'去结算' }}</button>
            </div>
        </div>
    </shop-foot>

    <div class="no" v-show="shop.length == 0">
      <p>购物车空空如也~</p>
      <van-button type="danger" size="large">去选购美食</van-button>
    </div>
  </div>
</template>

<script>
import shopList from '../components/shopList.vue'
import shopFoot from '../components/shopFoot.vue'
export default {
  data() {
    return {
      shop: JSON.parse(localStorage.getItem('shop')) || [],
      checked:false,
      status:false
    };
  },
  methods: {
    //删除
    del(id){
      let index = this.shop.findIndex((i)=> i.id == id)
      this.shop.splice(index,1)
    },
    //反选
    checkedFn(){
      this.checked = this.shop.every((i)=>{
        return i.flag == true
      })
    },
    //全选
    changeAll(){
      this.shop.forEach((i)=> i.flag = this.checked)
    },
    //编辑
    bj(){
      this.status = !this.status
    },
    //选中删除
    remove(){
      if(this.status == true){
        this.shop = this.shop.filter((i)=>{
          return i.flag == false
        })
      }
    }

  },
  computed: {
    sum(){
      let res = 0
      this.shop.forEach((i)=>{
        if(i.flag == true){
          res += i.num*i.minPrice
        }
      })
      return res
    }
  },
  filters: {},
  watch: {
    shop: {
      handler(newval) {
        localStorage.setItem('shop', JSON.stringify(newval))
      },
      deep: true
    }
  },
  components: {
    shopFoot,
    shopList
  }
};
</script>

<style lang="scss" scoped>

.head {
  width: 100%;
  padding: 10px 0;
  text-align: center;
}

.con {
  width: 100%;
  display: flex;
  justify-content: space-between;
  padding: 15px 10px;
  box-sizing: border-box;
  .s1 {
    color: #979693;
  }
}
.foot{
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: fixed;
    bottom: 50px;
    left: 0;
    text-align: center;
    .left{
      width: 50%;
      padding-left: 10px;
    }
    .right{
        width: 50%;
        .s1{
            color: #bb423d;
        }
        button{
            height: 50px;
            background-color: red;
            color: white;
            border: none;
            width: 100px;
        }
    }
}
.shop{
    width: 100%;
    display: flex;
    .itm{
         flex: 1;
    }
}
.van-card{
        background-color: #f1ebdc !important;
        border-bottom: 1px solid #eadfc8;
    }
    .delete-button{
        height: 100%;
    }


.no{
  margin-top: 200px;
  text-align: center;
  color: #94938d;
  .van-button{
    width:80%;
    border-radius: 5px;
  }
}
</style>