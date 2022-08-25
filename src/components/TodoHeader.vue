<template>
  <header class="header">
    <h1>todos</h1>
    <input id="toggle-all" class="toggle-all" type="checkbox" v-model="isAll">
    <label for="toggle-all"></label>
    <!-- 实现子传父 -->
    <!-- 目标：按下回车键，添加任务到父组件的list里 -->
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      @keydown.enter="dowFn"
      v-model="task"
    />
  </header>
</template>

<script>
export default {
  props: ['arr'],
  data() {
    return {
      task: ''
    };
  },
  methods: {
    dowFn() {
      // 将添加的任务名加入list数组
      this.$emit('create', this.task);
    }
  },
  computed: {
    isAll: {
      // 从按钮得到值
      set(checked) {
        // 全选按钮点击，value为true，set方法接收true
        // 实现点击全选按钮，影响数组内其它数据全选
        this.arr.forEach(obj => obj.isDone = checked)
      },
      // get里要返回的值-给这个计算属性具体值
      // 通过返回true|false ，来影响按钮是否选中
      get() {
        return this.arr.length !== 0 && this.arr.every(obj => obj.isDone === true)
      }
    }
  }
}
</script>