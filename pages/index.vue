<script lang="ts" setup>
import { ref } from "vue";

interface Workspace {
    id: Number
    name: String
}
const newWorkSpaceName = ref("");
const workspaceList = ref<Workspace[]>([]);
const createWorkSpace = () => {
    const randomId = Math.floor(Math.random() * 100);
    workspaceList.value.push(
        {
            id: randomId,
            name: newWorkSpaceName.value,
        }
    )
    newWorkSpaceName.value = "";
}
</script>

<template >
    <h1> Home page </h1>
    <h2> Recently viewed</h2>
    <h2> Workspaces </h2>
    <input type="text" v-model="newWorkSpaceName" @keyup.enter="createWorkSpace">
    <button @click.prevent = "createWorkSpace">Create a Workspace</button>
    <ul class="workspace-list">
        <li 
        v-for="workspace in workspaceList" 
        :key="workspace.id" class="workspace-card"
        >
        {{ workspace.id }} : {{ workspace.name }}
        </li>
    </ul>
</template>

<style>
    .workspace-card{
        display: block;
        border: 2px solid #222;
        border-radius: 4px;
        padding: 2rem;
        margin-bottom: 1rem;
    }
    .workspace-list{
        margin-left: 0;
        padding-left: 0;
    }

</style>