<template>
  <div>
    <div>
      <input type="text" @keyup.enter="handleClick" v-model="mytodo">
      <button @click="handleClick">添加</button>
      <button @click="clean">清空</button>
    </div>
    <ul>
      <li :class="{'done': todo.done}" @click="toggle(index)" v-for="(todo,index) in todoList" :key="index">{{index+1}} : {{todo.text}}</li>
    </ul>
    <p>{{remain}}/{{todoList.length}}</p>
  </div>
</template>

<script>
export default {
  data () {
    return {
      mytodo: '',
      todoList: [
        { text: '吃饭', done: false },
        { text: '睡觉', done: false },
        { text: '打豆豆', done: false }
      ]
    }
  },
  computed: {
    remain () {
      return this.todoList.filter(v => !v.done).length
    }
  },
  methods: {
    handleClick () {
      this.todoList.push({ text: this.mytodo, done: false })
      this.mytodo = ''
    },
    toggle (i) {
      this.todoList[i].done = !this.todoList[i].done
    },
    clean () {
      this.todoList = this.todoList.filter(v => !v.done)
    }
  }
}
</script>
<style>
  ul li.done {
    text-decoration: line-through;
    color: red;
  }
</style>
