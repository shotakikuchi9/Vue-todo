<template>
<table>
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
</template>
<script>
export default {
  props: ['tasks'],
  computed: {
    workingTasks: function() {
      return this.tasks.filter(task => task.state === '作業中')
    }
  },
  methods: {
    changeWorkingStatus(index) {
      this.workingTasks[index].state = '完了';
    },
    deleteWorkingTask(index) {
      const deletedTaskIndex = this.tasks.indexOf(this.workingTasks[index])
      this.workingTasks.splice(index,1);
      this.tasks.splice(deletedTaskIndex,1);
    }
  }
}
</script>