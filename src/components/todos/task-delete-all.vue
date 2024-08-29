<template>
    <a @click="deleteAlltask" class="bg-[#FC4852] px-2 py-1 cursor-pointer"><font-awesome-icon :icon="['fas', 'trash']" /><i class="fa-solid fa-trash"></i> Tasks</a>
</template>

<script>
export default {
    methods: {
        deleteAlltask() {
            this.$emit('deleteAlltask')
        }
    }
}
</script>