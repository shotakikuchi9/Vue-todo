<template>
    <div id="app">
      <h1>Todoリスト</h1>
      <p>{{currentStatus}}</p>
    <div>
      <label><input type="radio" value="全て" name="status" checked @click="currentStatus = '全て'">全て</label>
      <label><input type="radio" value="作業中" name="status" @click="currentStatus = '作業中'">作業中</label>
      <label><input type="radio" value="完了" name="status" @click="currentStatus = '完了'">完了</label>
    </div>
    <div>                       
      <!-- <table v-if="currentStatus === '全て'"> -->
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>コメント</th>
            <th>状態</th>
            <th></th>
          </tr>
        </thead>
        <tbody v-for="(task, index) in selectedTasks(currentStatus)" :key="index">
          <tr>
            <td>{{index}}</td>
            <td>{{task.content}}</td>
            <td><button @click="changeStatus(index)">{{task.state}}</button></td>
            <td><button @click="deleteTask(index)">削除</button></td>
          </tr>
        </tbody>
      </table>

      <!-- <table v-else-if="currentStatus === '作業中' ">
        <thead>
          <tr>
            <th>ID</th>
            <th>コメント</th>
            <th>状態</th>
            <th></th>
          </tr>
        </thead>
        <tbody v-for="(workingTask, index) in workingTasks" :key="index">
          <tr>
            <td>{{index}}</td>
            <td>{{workingTask.content}}</td>
            <td><button @click="changeWorkingStatus(index)">{{workingTask.state}}</button></td>
            <td><button @click="deleteWorkingTask(index)">削除</button></td>
          </tr>
        </tbody>
      </table>

      <table v-else-if="currentStatus === '完了'">
        <thead>
          <tr>
            <th>ID</th>
            <th>コメント</th>
            <th>状態</th>
            <th></th>
          </tr>
        </thead>
        <tbody v-for="(completeTask, index) in completeTasks" :key="index">
          <tr>
            <td>{{index}}</td>
            <td>{{completeTask.content}}</td>
            <td><button @click="changeCompleteStatus(index)">{{completeTask.state}}</button></td>
            <td><button @click="deleteCompleteTask(index)">削除</button></td>
          </tr>
        </tbody>
      </table> -->

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
    // workingTasks: function() {
    //   return this.tasks.filter(task => task.state === '作業中')
    // },
    //  completeTasks: function() {
    //    return this.tasks.filter(task => task.state === '完了');
    // }
    selectedTasks: function() {
      return function(currentStatus) {
        return this.tasks.filter(task => task.state === currentStatus)
      }
    }
  },
  methods: {
    addTask() {
      this.tasks.push({content: this.content, state: this.state});
      this.content = '';
    },
     deleteTask(index) {
      this.tasks.splice(index,1);
    },
    changeStatus(index) {
      if (this.tasks[index].state === '作業中') {
        this.tasks[index].state = '完了';
      } else if (this.tasks[index].state === '完了') {
        this.tasks[index].state = '作業中';
      }
    },
    changeWorkingStatus(index) {
      this.workingTasks[index].state = '完了';
    },
    deleteWorkingTask(index) {
      const deletedTaskIndex = this.tasks.indexOf(this.workingTasks[index])
      this.workingTasks.splice(index,1);
      this.tasks.splice(deletedTaskIndex,1);
    },
    changeCompleteStatus(index) {
      this.completeTasks[index].state = '作業中';
    },
    deleteCompleteTask(index) {
      const deletedTaskIndex = this.tasks.indexOf(this.completeTasks[index])
      this.completeTasks.splice(index,1);
      this.tasks.splice(deletedTaskIndex,1);
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
