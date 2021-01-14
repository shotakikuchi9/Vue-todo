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
  <tbody v-for="(completeTask, index) in completeTasks" :key="index">
    <tr>
      <td>{{index}}</td>
      <td>{{completeTask.content}}</td>
      <td><button @click="changeCompleteStatus(index)">{{completeTask.state}}</button></td>
      <td><button @click="deleteCompleteTask(index)">削除</button></td>
    </tr>
  </tbody>
</table>
</template>
<script>
export default {
  props: ['tasks'],
  computed: {
    completeTasks: function() {
       return this.tasks.filter(task => task.state === '完了');
    }
  },
  methods: {
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