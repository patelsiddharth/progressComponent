 <script setup>
import { ref } from 'vue';
import HelloWorld from './components/HelloWorld.vue';

const progressBarCount = ref([{
    index: 0,
    status: 'inprogress'
}]);

const refreshComponent = ref(Math.random())

function addProgressBar() {
    const len = progressBarCount.value.length;
    const obj = { index: len, status: '' }
    if(progressBarCount.value[len - 1].status === 'completed')
    {
        obj.status = 'inprogress';
    }
    progressBarCount.value.push(obj);
}

function reset() {
    progressBarCount.value = [{
        index: 0,
        status: 'inprogress',
    }];

    refreshComponent.value = Math.random();
}

function startNextProgress(progressItem) {
    progressItem.status = 'completed';
    if(progressBarCount.value[progressItem.index + 1])
    {
        progressBarCount.value[progressItem.index + 1].status = 'inprogress';
    }
    else
    {
        progressBarCount.value.push({
            index: progressItem.index + 1,
            status: 'inprogress',
        })
    }
}
</script>

<template>
    <h1>Progress Component</h1>
    <div class="progress-bar-container">
        <span :key="refreshComponent" v-for="(item, index) in progressBarCount">
            <HelloWorld 
                :key="index"
                :info="item"
                @complete="startNextProgress"
            />
        </span>
    </div>
    <div class="add-progress-bar-button">
        <button @click="addProgressBar">Add progress bar</button>
        <button @click="reset">Reset</button>
    </div>
</template>

<style>
.progress-bar-container {
    display: flex;
    flex-direction: column;
    gap: 10px;
    height: 400px;
    overflow-y: auto;
    justify-content: center;
}

.add-progress-bar-button {
    padding: 10px;
    display: flex;
    gap: 15px;
    justify-content: center;
}
</style>
