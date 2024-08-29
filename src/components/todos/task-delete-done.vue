<template>
    <a @click="deleteAllDoneTask()" class="bg-[#FC4852] px-2 py-[5px] cursor-pointer"><font-awesome-icon :icon="['fas', 'trash']" /> Tasks Done</a>
</template>

<script>
export default {
    methods: {
        deleteAllDoneTask() {
            this.$emit('deleteAllDoneTask')
        }
    }
}
</script>