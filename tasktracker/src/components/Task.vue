<template>
  <div>
    <div :class="[task.reminder ? 'reminder' : '', 'task']">
      <h3>
        {{ task.text }}
        <q-icon @click="onDelete(task.id)" name="close" />
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
  },
  methods: {
      onDelete(id){
        //   console.log(id)
        // emit to other component ,assign variable , parameter id
        this.$emit('delete-task', id)

      }
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
