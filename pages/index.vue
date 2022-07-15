<script setup>
import { ref } from "vue";
import { workspaceList } from '../store/global'


const newWorkSpaceName = ref("");
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
<div>
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
       <nuxt-link :to="`/workspace/${workspace.id}`">
            {{ workspace.id }} : {{ workspace.name }}
       </nuxt-link>
        </li>
    </ul>
</div>
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