<template>
    <div>
        <van-nav-bar title="商品详情"   left-arrow  @click-left="onClickLeft"/>
        <p>{{ basicInfo.name }}</p>
        <div class="box">
            <img :src="basicInfo.pic" alt="">
            <p class="p1">￥{{ basicInfo.minPrice }}</p>
        </div>
        <div class="box1">
            <span>购买数量</span>
            <van-stepper v-model="num" step="1" />
        </div>
        <div class="foot">
            <button class="qu" @click="toAbout">去结算</button>
            <button class="jia" @click="add">加入购物车</button>
        </div>
    </div>
</template>

<script>
import { Toast } from 'vant'
export default {
    data() {
        return {
            id: this.$route.query.id,
            basicInfo: {},
            num:1,
            shop:JSON.parse(localStorage.getItem('shop'))||[]
        };
    },
    methods: {
        getdetail() {
            this.$axios.get("https://api.it120.cc/noodles/shop/goods/detail?id=" + this.id).then((res) => {
                console.log(res, 'detail');
                this.basicInfo = res.data.data.basicInfo
            })
        },
        onClickLeft(){
            this.$router.go(-1)
        },
        toAbout(){
            this.$router.push('/about')
        },
        add(){
            let res = this.shop.find((i)=> i.id == this.basicInfo.id)
            Toast.success('内容已复制');
            if(res){
                res.num++
            }
            else{
                this.shop.push({...this.basicInfo,num:this.num,flag:false})
            }
        }
    },
    computed: {
       
    },
    filters: {},
    watch: {
        shop:{
            handler(newval){
                localStorage.setItem('shop',JSON.stringify(newval))
            },
            deep:true
        }
    },
    components: {},
    created() {
        this.getdetail()
    }
};
</script>

<style lang="scss" scoped>
.van-nav-bar{
    background-color: #f1ebdc !important;
}
p{
    padding-left: 15px;
}
.box{
    width: 100%;
    padding-top:10px ;
    border-top: 1px solid #e7d9bd;
    border-bottom: 1px solid #e7d9bd;
    img{
        width: 100%;
        height: 220px;
    }
    .p1{
        color: #d24742;
    }
}
.box1{
    width: 100%;
    display: flex;
    justify-content: space-between;
    padding: 25px 10px;
    box-sizing: border-box;
}
.foot{
    width: 100%;
    display: flex;
    justify-content: space-around;
    .qu{
        background-color: #18a219;
        color: white;
        border: none;
        padding: 10px;
        border-radius: 5px;
    }
    .jia{
        background-color: #e03a36;
        color: white;
        border: none;
        padding: 10px;
        border-radius: 5px;
    }
}
</style>