<template>
  <div>
    <slot></slot>
  </div>
</template>

<script>
export default {
  // provide返回对象可以跨层级传参给子孙
  provide () {
    return {
      form: this  //表单实例传递给后代
    };
  },
  props: {
    model: { type: Object, required: true },
    rules: { type: Object }
  },
  methods: {
    async validate (cb) {
      //执行表单中所有表单项校验

      const tasks = this.$children
        .filter(item => item.prop)
        .map(item => item.validate());  //task中是promise数组
      //task中任一false就校验失败
      console.log(tasks);
      const results = await Promise.all(tasks);//布尔值组成的数组
      if (results.some(valid => !valid)) {
        cb(false);
      } else {
        cb(true);
      }


    }
  }
}
</script>

<style scoped>
</style>


