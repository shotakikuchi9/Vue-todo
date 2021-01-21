<template>
    <div id="app">
      <h1>Todoリスト</h1>
    <div>
      <label><input type="radio" value="全て" name="status" checked @click="currentStatus = '全て'">全て</label>
      <label><input type="radio" value="作業中" name="status" @click="currentStatus = '作業中'">作業中</label>
      <label><input type="radio" value="完了" name="status" @click="currentStatus = '完了'">完了</label>
    </div>
    <div>                       
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>コメント</th>
            <th>状態</th>
            <th></th>
          </tr>
        </thead>
        <tbody v-for="(task, index) in selectedTasks" :key="index">
          <tr>
            <td>{{index}}</td>
            <td>{{task.content}}</td>
            <td><button @click="changeStatus(index)">{{task.state}}</button></td>
            <td><button @click="deleteTask(index)">削除</button></td>
          </tr>
        </tbody>
      </table>
      <h2>新規タスクの追加</h2>  
    </div>                          
    <div>  
      <input type="text" class="task" v-model="content">
      <button @click="addTask">追加</button>
    </div>
  </div>
</template>
<script>
export default {
  name: 'App',
  data() {
    return {
      tasks: [],
      content: '',
      state: '作業中',
      currentStatus: '全て'
    }
  },
  computed: {
    selectedTasks: function() {
      if(this.currentStatus === '全て') {
        return this.tasks
      } else {
        return this.tasks.filter(task => task.state === this.currentStatus)
      }
    }
  },
  methods: {
    addTask() {
      this.tasks.push({content: this.content, state: this.state});
      this.content = '';
    },
     deleteTask(index) {
      if(this.currentStatus === '全て') {
        this.tasks.splice(index,1)
      } else {
        const selectedTaskIndex = this.tasks.indexOf(this.selectedTasks[index])
        this.selectedTasks.splice(index,1);
        this.tasks.splice(selectedTaskIndex,1);
      }

    },
    changeStatus(index) {
      if (this.selectedTasks[index].state === '作業中') {
        this.selectedTasks[index].state = '完了';
      } else if (this.selectedTasks[index].state === '完了') {
        this.selectedTasks[index].state = '作業中';
      }
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

