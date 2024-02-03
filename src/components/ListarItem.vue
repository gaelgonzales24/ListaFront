<script setup>
import { reactive } from 'vue';
import InputNew from './NuevoItem.vue';

let boards =  reactive([
    {
        id: crypto.randomUUID(),
        name: "tablero 1",
        items: [],
    },
]);
function newBoard(){
    const name = prompt('Nombre del nuevo tablero');
    if (!!name){
        boards.push({
            id: crypto.randomUUID(),
            name: name,
            items: [],
        });
    }
}

function newItem(text, board) {
    board.items.push({
        id: crypto.randomUUID(),
        title: text.value,
    });
}

function removeItem(board, item){
   const index = board.items.indexOf(item);
   if(index !== -1){
       board.items.splice(index, 1);
   }

 }
</script>

<template>
<nav>
    <ul>
        <li><a href="" @click.prevent="newBoard">Crear Tablero</a></li>
    </ul>
</nav>

<div class="boards-container">
    <div class="boards">
        <div 
            class="board"
            v-for="board in boards">
            <div>{{ board.name }}</div>
            <InputNew @on-new-item="(text)=>newItem(text, board)"/>
            <div class="items">
                <div 
                    class="item" 
                    draggable="true" 
                    @click="removeItem(board, item)"
                    v-for="item in board.items">
                    {{ item.title }}
                </div>
            </div>
        </div>
    </div>
</div>
</template>

<style scoped>
nav {
    background-color: black;
    margin-bottom: 10px;
}

nav ul{
    list-style: none;
    padding: 0;
    margin: 0;
    display: flex;
}

nav ul li a {
    display: block;
    padding: 10px;
    color: white;
    text-decoration: none;
}
.boards {
    display: flex;
    gap: 10px;
}
.board{
    background: #efefef;
    padding: 10px;
}
.items {
    display: flex;
    flex-direction: column;
    gap: 5px;
}
.item {
    background-color: white;
    padding: 10px;
    box-sizing: border-box;
}
</style>