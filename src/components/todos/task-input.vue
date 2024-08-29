<template>
    <input v-model="LocalTaskName" type="text" class="w-full rounded-full p-3 pr-12 outline-[#476CAC] border-2 border-[#476CAC]" placeholder="New Task">
</template>

<script>
export default {
    props: {
        task: {
            type: Object,
            required: true
        }
    },
    data() {
        return {
            LocalTaskName: this.task.name
        }
    },
    watch: {
        LocalTaskName(newName){
            this.$emit('newTaskName', newName)
        }
    }
    
}
</script>