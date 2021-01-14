<template>
  <div id="app">
      <h1>Todoリスト</h1>
    <div>
      <label><input type="radio" value="全て" name="status" checked @click="currentStatus = 'All'">全て</label>
      <label><input type="radio" value="作業中" name="status" @click="currentStatus = 'Working'">作業中</label>
      <label><input type="radio" value="完了" name="status" @click="currentStatus = 'Complete'">完了</label>
    </div>
    <div>          
      <component :is="currentStatus" :tasks="tasks"></component>
    </div>
    <div>                       
      <h2>新規タスクの追加</h2>  
    </div>                          
    <div>  
      <input type="text" class="task" v-model="content">
      <button @click="addTask">追加</button>
    </div>
  </div>
</template>
<script>
import Complete from './components/Complete'
import Working from './components/Working'
import All from './components/All'

export default {
  name: 'App',
  components: {
    Complete,
    Working,
    All
  },
  data() {
    return {
      tasks: [],
      content: '',
      state: '作業中',
      currentStatus: 'All'
    }
  },
  methods: {
    addTask() {
      this.tasks.push({content: this.content, state: this.state});
      this.content = '';
    }
  }
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.task {
  margin-right: 12px;
}
</style>
