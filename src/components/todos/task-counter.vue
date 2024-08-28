<template>
    <p class="bg-[#476CAC] rounded-full pl-2 pr-[4px] py-1">Tasks <span class="bg-white rounded-full text-[#476CAC] px-[6px]">{{ taskCounter }}</span></p>
</template>

<script>
export default {
    props: {
        taskCounter: {
            type: Number,
            required: true
        }
    }
}
</script>
