<template>
    <div>
        <p>Double click to tog  gle task reminder</p>
        <div :key="task.id" v-for="task in tasks">
                <Task
                    @toggle-reminder="$emit('toogle-reminder',  task.id)"
                    @delete-task="$emit('delete-task', task.id)"
                    :task="task"
                />
        </div>
    </div>
    
</template>

<script>
import Task from './Task.vue'

export default {
    name: 'Tasks',
    props: {
        tasks: Array,
    },
    components: {Task},
    emits: ['delete-task', 'toogle-reminder']
}
</script>

<style scoped>
p{
   color: #606B63; 
}
</style>