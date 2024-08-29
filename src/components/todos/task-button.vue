<template>
    <button @click="newTask" class="absolute right-4 top-1/2 transform -translate-y-1/2">
        <font-awesome-icon :icon="['fas', 'circle-plus']" class="text-3xl text-[#476CAC]" />
    </button>
</template>

<script>
export default {
    methods: {
        newTask() {
            this.$emit('newTask')
        }
    }
}
</script>
