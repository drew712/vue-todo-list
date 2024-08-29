<template>
    <li  
    :class="['border-2 rounded p-2 mb-2 relative hover:bg-[#E5E7EB]', { 'line-through text-[#808080]': task.done }]"
    v-on:mouseenter="isHovered = true"
    v-on:mouseleave="isHovered = false"
    >
        <font-awesome-icon 
        :icon="['fas', 'circle-check']" 
        @click="taskDone(task.id)" 
        :class="['text-[#41B883] cursor-pointer', { 'text-[#808080]': task.done }]" 
        />
        {{ task.name }} 
        <font-awesome-icon 
        :icon="['fas', 'trash']" 
        class="text-[#FC4852] right-4 absolute top-1/2 transform -translate-y-1/2 cursor-pointer"
        v-show="isHovered"
        @click="deleteTask(task.id)"
        />
    </li>
</template>

<script>
export default {
    props: {
        task: {
            type: Object,
            required: true
        }
    },
    data(){
        return {
            isHovered: false
        }
    },
    methods: {
        taskDone(id){
            this.$emit('taskDone', id)
        },
        deleteTask(id){
            this.$emit('deleteTask', id)
        }
    }
}
</script>
