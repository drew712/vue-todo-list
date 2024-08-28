<template>
    <p class="bg-[#476CAC] rounded-full pl-2 pr-[4px] py-1">Tasks Done <span class="bg-white rounded-full text-[#476CAC] px-[6px]">{{ tasksDoneCounter }}</span></p>
</template>

<script>
export default {
    props: {
        tasksDoneCounter: {
            type: Number,
            required: true
        }
    }
}
</script>