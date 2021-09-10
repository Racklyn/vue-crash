<template>
    <header>
        <h1><i class="far fa-sticky-note"/> {{title}}</h1>
        <Button
            v-show="homePage"
            @bnt-click="$emit('toggle-add-task')"
            :text="showAddTask ? 'Close' : 'Add Task'"
            :color="showAddTask ? 'red':'#21897E'"
        />
    </header>
</template>


<script>
import Button from './Button.vue'

export default {
    name: 'Header',
    props: {
        title: String,
        showAddTask: Boolean
    },
    components: {Button},
    computed: {
        homePage(){
            return this.$route.path === '/'
        }
    },
    emits: ['toggle-add-task']
}
</script>


<style scoped>
    header{
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
    .far{
        color: #8980F5;
    }
    
</style>