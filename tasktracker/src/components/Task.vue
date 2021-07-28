<template>
  <div>
    <div  v-on:click="$emit('toggle-reminder', task.id)" 
    :class="[task.reminder ? 'reminder' : '', 'task']">
      <h3>
        {{ task.text }}
        <q-icon @click="$emit('delete-task', task.id)" name="close" />
      </h3>

      <p>{{ task.day }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: Object
  }
};
</script>

<style scope>
.fas {
  color: red;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
