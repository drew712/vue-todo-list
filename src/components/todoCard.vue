<template>
    <div class="bg-gradient-to-t from-[#34495E] to-[#41B883]">    
      <div class="flex flex-col items-center justify-center min-h-screen">
          <h2 class="text-white text-[60px] text-center mb-2 font-bold">{{ title }}</h2>
          <div class="bg-[#FCFCFF] h-[300px] w-full max-w-[550px] flex flex-col justify-between">
              <div class="flex justify-end bg-[#E6E6DF] p-2 gap-2 text-white">
                  <p class="bg-[#476CAC] rounded-full pl-2 pr-[4px] py-1">Tasks <span class="bg-white rounded-full text-[#476CAC] px-[6px]">{{ taskCounter }}</span></p>
                  <p class="bg-[#476CAC] rounded-full pl-2 pr-[4px] py-1">Tasks Done <span class="bg-white rounded-full text-[#476CAC] px-[6px]">{{ tasksDoneCounter }}</span></p>
                  <div v-if="tasksDoneCounter >= 1" class="pt-1">
                    <a v-on:click="deleteAllDoneTask" class="bg-[#FC4852] px-2 py-[5px] cursor-pointer"><font-awesome-icon :icon="['fas', 'trash']" /> Tasks Done</a>
                  </div>
                  <a v-on:click="deleteAlltask" class="bg-[#FC4852] px-2 py-1 cursor-pointer"><font-awesome-icon :icon="['fas', 'trash']" /><i class="fa-solid fa-trash"></i> Tasks</a>
              </div>
              <div class="m-4 h-[250px] overflow-auto">
                  <ul>
                      <li 
                        v-for="task in tasks" 
                        :key="task.id" 
                        :class="['border-2 rounded p-2 mb-2 relative hover:bg-[#E5E7EB]', { 'line-through text-[#808080]': task.done }]"
                        v-on:mouseenter="task.isHovered = true"
                        v-on:mouseleave="task.isHovered = false"
                      >
                          <font-awesome-icon 
                            :icon="['fas', 'circle-check']" 
                            v-on:click="taskDone(task.id)" 
                            :class="['text-[#41B883] cursor-pointer', { 'text-[#808080]': task.done }]" 
                          />
                          {{ task.name }} 
                          <font-awesome-icon 
                            :icon="['fas', 'trash']" 
                            class="text-[#FC4852] right-4 absolute top-1/2 transform -translate-y-1/2 cursor-pointer"
                            v-show="task.isHovered"
                            v-on:click="deleteTask(task.id)"
                          />
                      </li>
                  </ul>
              </div>
              <div class="bg-[#E6E6DF] p-4">
                  <div class="relative w-full">
                      <input v-model="newTaskName" type="text" class="w-full rounded-full p-3 pr-12 outline-[#476CAC] border-2 border-[#476CAC]" placeholder="New Task">
                      <button v-on:click="newTask" class="absolute right-4 top-1/2 transform -translate-y-1/2">
                          <font-awesome-icon :icon="['fas', 'circle-plus']" class="text-3xl text-[#476CAC]" />
                      </button>
                  </div>
              </div>
          </div>
      </div>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            title: 'Vue ToDo List',
            tasks: [],
            newTaskName: '',
            newTaskId: 1,
            taskCounter: 0,
            tasksDoneCounter: 0
        }
    },
    methods: {
        newTask() {
            if (this.newTaskName.trim() === "") return;
  
            const newTask = {
                id: this.newTaskId,
                name: this.newTaskName,
                done: false,
                isHovered: false
            };
  
            this.tasks.push(newTask);
            this.taskCounter++;
            this.newTaskId++;
            this.newTaskName = "";
        },
        taskDone(taskId) {
            const task = this.tasks.find(task => task.id === taskId);
            if (task) {
                task.done = !task.done;
                this.tasksDoneCounter = this.tasks.filter(task => task.done).length;
            }
        },
        deleteTask(taskId) {
            this.tasks = this.tasks.filter(task => task.id !== taskId);
            this.taskCounter = this.tasks.length;
            this.tasksDoneCounter = this.tasks.filter(task => task.done).length;
        },
        deleteAlltask() {
            this.tasks = [];
            this.taskCounter = 0;
            this.tasksDoneCounter = 0;
        },
        deleteAllDoneTask() {
            this.tasks = this.tasks.filter(task => !task.done);
            this.taskCounter = this.tasks.length;
            this.tasksDoneCounter = 0;
        }
    }
}
</script>
  
<style>

</style>
