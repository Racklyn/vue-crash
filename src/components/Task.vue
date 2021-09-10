<template>
    <div
        @dblclick="$emit('toggle-reminder', task.id)"
        :class="['task', task.reminder ? 'reminder' : '']"
    >
        <h3>
            {{task.text}}
            <i @click="$emit('delete-task', task.id)" class="fas fa-times"></i>
        </h3>
        <p> {{task.day}} </p>
    </div>
</template>

<script>
export default {
    name: 'Task',
    props: {
        task: Object
    },
    emits:['delete-task', 'toggle-reminder']
}
</script>

<style scoped>
.fas {
  color: red;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
  border-radius: 0px 8px 8px 0px;
  
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.task.reminder {
  border-left: 5px solid #3BA99C;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>