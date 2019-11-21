<template>
  <div class="hello">
    <!-- 条件-->
    <p :title="title" v-if="title">{{title}}</p>
    <!-- 循环 -->
    <ul>
      <li v-for="good in goods" :key="good.id">
        <span>{{good.text}}</span>
        <span>￥{{good.price}}</span>
        <button @click="addCart(good)">加购物车</button>
      </li>
    </ul>
    <!-- 用户输入 -->
    <div>
      <input type="text" v-model="text">
      <button @click="addgood">添加商品</button>
    </div>
    <!-- 购物车 -->
    <Cart title="购物车" ref="Cart" @addCart="onAddCart"></Cart>
  </div>
</template>

<script>
import Cart from "./Cart.vue";
export default {
  name: "HelloWorld",
  components: {
    Cart
  },
  data () {
    return {
      title: "",
      text: "",
      goods: [
        { id: 1, text: "衬衫", price: 99 },
        { id: 2, text: "牛仔裤", price: 298 }
      ]
    };
  },
  created () {
    setTimeout(() => {
      this.title = "我的购物车";
    }, 1000);
  },
  methods: {
    addgood () {
      if (this.text) {
        this.goods.push({
          id: this.goods.length + 1,
          text: this.text,
          price: 98
        });
        this.text = "";
      }
    },
    addCart (good) {
      this.$refs.Cart.addCart(good);
    },
    onAddCart () {
      console.log('添加成功');
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
