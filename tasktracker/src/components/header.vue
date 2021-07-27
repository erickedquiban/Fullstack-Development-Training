<template>
<div>
    <h3>{{ title }}</h3>
    <Button text ="Add Tsk" color="green"/>
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