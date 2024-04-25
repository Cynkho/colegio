<script setup>
import { ref } from 'vue';
import IconDelete from './icons/IconDelete.vue';

defineProps(['text'])
const isDone = ref(false)

</script>

<template>
<li :class="{ 'is-done': isDone }">
    <input v-model="isDone" type="checkbox">
    <span>{{ text }}</span>
    <IconDelete @click="$emit('delete')"/>
</li>
</template>

<style scoped>

li {
    display: flex;
    column-gap: 6px;
}

.is-done {
    text-decoration: line-through;
    color: gray;
}

</style>