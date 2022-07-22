<template>

<div class="test-container">
  <h3>Test.vue组件</h3>
</div>

</template>

<script>
export default{
  props:['info'],
  data(){
    return {
      message:'hello'
    }
  },
  methods:{
    show(){
      console.log('调用了Test组件的show方法')
    },
    //使用Ajax请求图书列表的数据
    initBookList(){
      const xhr = new XMLHttpRequest()
      xhr.addEventListener('load',function(){
        const result = JSON.parse(xhr.responseText)
        console.log(result)
      })
      xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks')
      xhr.send();

    }
    
  },
  //创建阶段的第一个生命周期函数
  beforeCreate(){
    console.log(this.info)
    console.log(this.message)
    this.show()

  },
  created() {
    console.log(this.info)
    console.log(this.message)
    this.show()
    
  },

}

</script>


<style lang="less" scoped>
.test-container{
  background-color: pink;
  height: 200px;

}





</style>