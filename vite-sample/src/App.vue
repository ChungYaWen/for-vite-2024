<script setup>
import {ref}from 'vue';
const num=ref(2);
function clikcme(){
  num.value++
}
</script>

<template>
 <div> 
  
 <button type="button" v-on:click="clikcme">點我:</button>{{num}}
 </div>

</template>
