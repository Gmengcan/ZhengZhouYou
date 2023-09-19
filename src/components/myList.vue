<template>
    <div @click="todetail(item.id)">
        <img :src="item.pic" alt="">
        <p>{{ item.name }}</p>
        <span>￥{{ item.originalPrice }}</span>
    </div>
</template>

<script>
export default {
  props:['item'],
  data() {
     return {};
  },
  methods: {
    todetail(id){
        this.$emit('todetail',id)
    }
  },
  computed: {},
  filters: {},
  watch: {},
 components: {}
};
</script>

<style lang="scss" scoped>
img{
    width: 100%;
    height: 165px;
    border-radius:5px 5px 0 0;
}
p{
    padding-left:10px ;
}
span{
    color: #d53835;
    padding-left:10px ;
}
</style>