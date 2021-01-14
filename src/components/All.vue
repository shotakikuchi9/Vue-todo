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
  <tbody v-for="(task, index) in tasks" :key="index">
    <tr>
      <td>{{index}}</td>
      <td>{{task.content}}</td>
      <td><button @click="changeStatus(index)">{{task.state}}</button></td>
      <td><button @click="deleteTask(index)">削除</button></td>
    </tr>
  </tbody>
</table>
</template>
<script>
export default {
  props: ['tasks'],
  methods: {
    deleteTask(index) {
      this.tasks.splice(index,1);
    },
    changeStatus(index) {
      if (this.tasks[index].state === '作業中') {
        this.tasks[index].state = '完了';
      } else if (this.tasks[index].state === '完了') {
        this.tasks[index].state = '作業中';
      }
    }
  }
}
</script>