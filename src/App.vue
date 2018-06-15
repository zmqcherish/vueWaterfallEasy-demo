<template>
   <vue-waterfall-easy :imgsArr="imgsArr" class="container" @scrollReachBottom="getData"></vue-waterfall-easy>
</template>

<script>

  import vueWaterfallEasy from 'vue-waterfall-easy'
  import axios from 'axios'
  export default {
  name: 'app',
  data() {
    return {
      imgsArr: [],
      group: 0, // request param
    }
  },
  components: {
    vueWaterfallEasy
  },
  methods: {
    getData() {
      axios.get('./static/mock/data.json?group=' + this.group) // 真实环境中，后端会根据参数group返回新的图片数组，这里我用一个惊呆json文件模拟
        .then(res => {
          console.log(res.data);
          this.imgsArr = this.imgsArr.concat(res.data)
          this.group++
        })
    },
  },
  created() {
    this.getData()
  }
}
</script>
<style>
.container {
  position: absolute;
  width: 100%;
  box-sizing: border-box;
  min-height: 100%;
}
</style>

