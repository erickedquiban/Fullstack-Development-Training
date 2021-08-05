<template>
        <q-btn @click="onClick()" :style="{background: color}" class="btn">{{text}} </q-btn>
</template>

<script>
export default {
    name: 'Button',
    props: {
        text: String,
        color: String,
    },
    methods:{
        onClick(){
          this.$emit('btn-click')
        }
    }
}

</script>

<style  scoped>

</style>
