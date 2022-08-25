<template>
  <footer class="footer">
    <span class="todo-count">剩余<strong>{{count}}</strong></span>
    <ul class="filters" @click="showFn">
      <li>
        <a :class="{selected : status === 'all'}" href="javascript:;" @click="status='all'">全部</a>
      </li>
      <li>
        <a :class="{selected : status === 'no'}" href="javascript:;" @click="status='no'">未完成</a>
      </li>
      <li>
        <a :class="{selected : status === 'yes'}" href="javascript:;" @click="status='yes'">已完成</a>
      </li>
    </ul>
    <button class="clear-completed" @click="clearFn">清除已完成</button>
  </footer>
</template>

<script>
export default {
  data() {
    return {
      status: 'all'
    }
  },
  props: ['data'],
  computed: {
    count() {
      return this.data.length
    }
  },
  methods: {
    showFn() {
      this.$emit('show', this.status)
    },
    clearFn() {
      this.$emit('clear')
    }
  }
}
</script>