<template>
  <div class="test-container">
    <h3 id="myh3">Test.vue组件--{{ books.length }}本图书</h3>
    <p id="p1">message的值：{{message}}</p>
    <button @click="message += '~'">修改message的值</button>
  </div>
</template>

<script>
export default {
  props: ["info"],
  data() {
    return {
      message: "hello",
      //定义books数组，存储所有图书数组，默认为空
      books: "",
    };
  },
  methods: {
    show() {
      console.log("调用了Test组件的show方法");
    },
    //使用Ajax请求图书列表的数据
    initBookList() {
      const xhr = new XMLHttpRequest();
      xhr.addEventListener("load", () => {
        const result = JSON.parse(xhr.responseText);
        this.books = result.data;
      });
      xhr.open("GET", "http://www.liulongbin.top:3006/api/getbooks");
      xhr.send();
    },
  },
  //创建阶段的第一个生命周期函数
  beforeCreate() {
    // console.log(this.info)
    // console.log(this.message)
    // this.show()
  },
  created() {
    //非常常用，经常在里面调用methods方法，请求服务器的数据，转存到data中
    // console.log(this.info)
    // console.log(this.message)
    // this.show()
    this.initBookList();
  },
  beforeMount() {
    // console.log('beforeMount')
    // // this.initBookList()
    // const dom = document.querySelector("#myh3");
    // console.log(dom);
  },
  //如果要操作当前组件的dom，最早在mounted进行
  mounted(){
    // console.log(this.$el)
    // const dom = document.querySelector("#myh3");
    // console.log(dom);
  },
  beforeUpdate(){
    // console.log('beforeUpdate')

    // console.log(this.message)
    // const dom = document.querySelector("p1");
    // console.log(dom.innerHTML)
  },
  //当数据变化之后，为了能够操作最新的DOM结构,应该在updated中进行
  updated() {
    console.log(this.message)
    const dom = document.querySelector("p1");
    console.log(dom.innerHTML)
  },
};
</script>


<style lang="less" scoped>
.test-container {
  background-color: pink;
  height: 200px;
}
</style>