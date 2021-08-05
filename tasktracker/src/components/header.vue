<template>
<div>
    <h3>{{ title }}</h3>
    <Button @btn-click="$emit('toggle-add-task')" 
    :text ="showAddTask ? 'Close' : 'Add Task'" 
    :color="showAddTask ? 'red': 'green' "/>
</div>
</template>

<script>
 import Button from './Button'
 
export default {
    components: {
    Button,
  },
    name: 'Header',
    props: {
        title: String,
        showAddTask: Boolean
    }
}
</script>

<style scoped>

header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}
</style>