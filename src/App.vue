<template>
  <section class="todoapp">
    <!-- 除了驼峰, 还可以使用-转换链接 -->
    <TodoHeader :arr="list" @create="createFn"></TodoHeader>
    <TodoMain :arr="showArr" @del="delFn"></TodoMain>
    <TodoFooter :data="list" @show="showFn" @clear="clearFn"></TodoFooter>
  </section>
</template>

<script>
// 目标：1.创建工程-准备相关组件文件
// 1.0样式引入
import "./styles/base.css"
import "./styles/index.css"
// 1.1组件引入
import TodoHeader from "./components/TodoHeader";
import TodoMain from "./components/TodoMain";
import TodoFooter from "./components/TodoFooter";


export default {
  // 1.3组件注册
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  // 目标：2.铺设待办任务-父传子数据
    // 首先：将list数据给arr变量，设置在子组件面板上
    // 子组件通过prop属性，绑定获取的arr变量
    // 循环遍历arr数组的值，展示到页面
  data() {
    return {
      // 8.1 默认从本地取值
      list: JSON.parse(localStorage.getItem('todoList')) || [],
      getSel: 'all'
    };
  },
  // 函数
  methods: {
    createFn(taskName) {
      let id = this.list.length == 0 ? 100 : this.list[this.list.length - 1].id + 1
      this.list.push({
        id: id,
        name: taskName,
        isDone: false
      })
    },
    delFn(id) {
      let index = this.list.findIndex(obj => obj.id === id)
      this.list.splice(index, 1)
    },
    showFn(status) {
      this.getSel = status
    },
    clearFn() {
      this.list = this.list.filter(obj => obj.isDone === false)
    }
  },
  // 计算属性
  computed: {
    showArr() {
      if(this.getSel === 'yes') {
        return this.list.filter(obj => obj.isDone === true)
      }else if (this.getSel === 'no') {
        return this.list.filter(obj => obj.isDone === false)
      }else {
        return this.list

      }
    }
  },
  // 开启监听list的变化
  // 8. 目标: 数据缓存
  watch: {
    list: {
      deep: true,
      handler(){
          // 8.0 只要list变化 - 覆盖式保存到localStorage里
          localStorage.setItem('todoList', JSON.stringify(this.list))
      }
    }
  }
};
</script>