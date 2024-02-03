<script setup>
import {ref, defineEmits } from "vue";

const text = ref("");
const emits = defineEmits(["onNewItem"]);

function Submit() {
    if (text != "") {
        emits("onNewItem", text);
        text.value="";
    }
}
</script>

<template>
    <form action="" @submit.prevent="Submit">
        <input type="text" v-model="text">
        <input type="submit" value="Enviar">
    </form>
</template>

<style scoped>

</style>
