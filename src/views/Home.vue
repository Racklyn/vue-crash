<template>
    <AddTask
        @add-task="addTask"
        v-show="showAddTask"
    />
    <Tasks
      @toogle-reminder="toggleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
    />
</template>

<script>
import Tasks from '../components/Tasks.vue'
import AddTask from '../components/AddTask.vue'

export default{
    name: 'Home',
    props: {
        showAddTask: Boolean
    },
    components: {Tasks, AddTask},
    data() {
        return{
            tasks: []
        }
    },
    methods: {
        async addTask(newTask){
        try {
            const res = await fetch('api/tasks', {
            method: 'POST',
            headers: {
                'Content-type': 'application/json',
            },
            body: JSON.stringify(newTask)
            })

            const data = await res.json() //retorna o obj adicionado

            this.tasks = [...this.tasks, data]

        } catch (error) {
            alert('Error!')
            console.log(error)
        }

        },
        async deleteTask(id){
        if(confirm('Are you sure?')){
            const res =  await fetch(`api/tasks/${id}`, {
            method: 'DELETE'
            })

            if (res.status === 200){
            this.tasks = this.tasks.filter((task) =>task.id != id)
            }else{
            alert("Error deleting task!")
            }
        }
        },
        async toggleReminder(id){
        const taskToToggle = await this.fetchTask(id)
        const updTask = {...taskToToggle, reminder: !taskToToggle.reminder}

        try {
            const res = await fetch(`api/tasks/${id}`,{
            method: 'PUT',
            headers: {
                'Content-type': 'application/json'
            },
            body: JSON.stringify(updTask)
            })

            const data = await res.json() //retorna obj atualizado

            this.tasks = this.tasks.map(task => 
            task.id === id ? {...task, reminder: data.reminder} : task
            )
        } catch (error) {
            alert('Error!')
            console.log(error)
        }
        
        },
        async fetchTasks(){
        let data = []

        try {
            const res = await fetch('api/tasks')  

            data = await res.json()
        } catch (error) {
            alert("Erro com o servidor")
            console.log(error )
        }
        

        return data
        },
        async fetchTask(id){
            let data = {}

            try {
                const res = await fetch(`api/tasks/${id}`)  

                data = await res.json()
            } catch (error) {
                alert("Erro com o servidor")
                console.log(error )
            }
        

            return data
        }
    },

  
  //Função executada quando o componente for criado (tipo useEffect)
  async created(){
    this.tasks = await this.fetchTasks()
  }
}

</script>