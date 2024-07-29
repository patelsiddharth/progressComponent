<script setup>
import { ref, onMounted } from 'vue';
const props = defineProps(['info'])

const emit = defineEmits(['complete'])

const count = ref(0);

onMounted(() => {
    const interval = setInterval(() => {
        if(props.info.status === 'inprogress')
        {
            if(count.value < 100)
            {
                count.value += 1;
            }
            else
            {
                clearInterval(interval);
                emit('complete', props.info);
            }
        }
    }, 100);
});
</script>

<template>
    <progress
        id="progress-id"
        :value="count"
        max="100"
    ></progress>
</template>

<style>
.read-the-docs {
    color: #888;
}
</style>