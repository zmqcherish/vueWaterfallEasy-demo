<template>
   <vue-waterfall-easy :imgsArr="imgsArr" @scrollReachBottom="getData"></vue-waterfall-easy>
</template>

<script>

  import vueWaterfallEasy from 'vue-waterfall-easy'
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
      $.get('./static/mock/data.json?group=' + this.group) // 真实环境中，后端会根据参数group返回新的图片数组，这里我用一个惊呆json文件模拟
        .then(res => {
          console.log(res);
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
