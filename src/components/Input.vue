<script setup>
const props = defineProps(["word","placeholder"])

const emits = defineEmits(["update:word"])

const wordHandler = (event) => {
    emits("update:word", event.target.value)
}

</script>

<template>
    <input type="text" :value="props.word" class="word" :placeholder="props.placeholder" @input="wordHandler">
</template>

<style scoped>
    .word{
        width: 384px;
        height: 30px;
        border: transparent;
    }
    .word:focus{
        outline: none;
    }
</style>