
<script>
import { workspaceList } from "../../store/global"
    export default {
        setup() {
            return {
                workspaceList
            }
        },
        data: () =>  ({
            workspaceName: '',
            board: {
            columns: [],
            newCardItem: '',
           }
        }),
        mounted() {
            this.workspaceName = this.workspaceList.find((workspace) => workspace.id === Number(this.$route.params.id)).name;
        },
        methods: {
            createColumn() {
                this.board.columns.push(
                    {
                        newItemName: '',
                        items: []
                    }
                )
            },
            createCard(column) {
                if(column.newItemName === '') return false;
                column.items.push({  
                    id: 123,
                    name: column.newItemName
                })
                column.newItemName = '';
            }
        }
    }
</script>

<template>
        <div>
            <h1>{{ workspaceName }} Workspace (#{{ $route.params.id }})</h1>
            <section>
                <h2> {{ board.name }} </h2>
                <button @click="createColumn">Create Column</button>
                <div class="column-grid">
                    <section class="board-column" v-for="(column, index) in board.columns" :key="column[index]">
                        <input type="text" v-model="column.newItemName" @keyup.enter="createCard(column)">
                        <button @click="createCard(column)">Create a card</button>
                        <ul >
                                <li v-for="item in column.items" :key="item.id">
                                    {{ item.name }}
                                </li>
                        </ul>
                    </section>
                </div>
            </section>
            
        </div>
</template>
<style>
    .column-grid {
        display: grid;
        grid-template-columns: repeat(v-bind(board.columns.length), 1fr);
    }
    .board-column{
        border: 1px solid #222;
        height: 80vh;
        margin-right: 1rem;
    }
   
</style>