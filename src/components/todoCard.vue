<template>
    <div class="bg-gradient-to-t from-[#34495E] to-[#41B883]">    
      <div class="flex flex-col items-center justify-center min-h-screen">
          <h2 class="text-white text-[60px] text-center mb-2 font-bold">{{ title }}</h2>
          <div class="bg-[#FCFCFF] h-[300px] w-full max-w-[550px] flex flex-col justify-between">
              <div class="flex justify-end bg-[#E6E6DF] p-2 gap-2 text-white">
                    <TaskCounter :taskCounter="taskCounter" />
                    <TaskCounterDone :tasksDoneCounter="tasksDoneCounter"/>
                    <DeleteTaskDone 
                    v-if="tasksDoneCounter >= 1"
                    @deleteAllDoneTask="deleteAllDoneTask"/>
                    <DeleteTaskAll @deleteAlltask="deleteAlltask" />  
              </div>
              <div class="m-4 h-[250px] overflow-auto">
                  <ul>
                    <TaskItem 
                        v-for="task in tasks" 
                        :key="task.id"
                        :task="task"
                        @taskDone="taskDone"
                        @deleteTask="deleteTask"
                    />
                  </ul>
              </div>
              <div class="bg-[#E6E6DF] p-4">
                  <div class="relative w-full">
                        <TaskInput :task="task" @newTaskName="newTaskName"/>
                        <TaskButton @newTask="newTask"/>
                  </div>
              </div>
          </div>
      </div>
    </div>
</template>
  
<script>
import TaskCounter from './todos/task-counter.vue'
import TaskItem from './todos/task-item.vue'
import TaskCounterDone from './todos/task-counter-done.vue'
import DeleteTaskDone from './todos/task-delete-done.vue'
import DeleteTaskAll from './todos/task-delete-all.vue'
import TaskInput from './todos/task-input.vue'
import TaskButton from './todos/task-button.vue'

const task = {
    id: 1,
    name: '',
    done: false
};

export default {
    components:{
       TaskCounter,
       TaskItem,
       TaskCounterDone,
       DeleteTaskDone,
       DeleteTaskAll,
       TaskInput,
       TaskButton
    },
    data() {
        return {
            title: 'Vue ToDo List',
            tasks: [],
            task: {...task}
        }
    },
    computed:{
        taskCounter(){
            return this.tasks.length;
        },
        tasksDoneCounter(){
            return this.tasks.filter(task => task.done).length;
        }
    },
    methods: {
        newTaskName(newName) {
        this.task.name = newName; 
        },
        newTask() {
            if (this.task.name.trim() === "") return;
  
            const newTask = {
                id: this.tasks.length + 1,
                name: this.task.name,
                done: false,
            };
  
            this.tasks.push(newTask);
            this.task = {...task};
        },
        taskDone(taskId) {
            const task = this.tasks.find(task => task.id === taskId);
            if (task) {
                task.done = !task.done;
            }
        },
        deleteTask(taskId) {
            this.tasks = this.tasks.filter(task => task.id !== taskId);
        },
        deleteAlltask() {
            this.tasks = [];
        },
        deleteAllDoneTask() {
            this.tasks = this.tasks.filter(task => !task.done);
        }
    }
}
</script>
  
<style>

</style>
