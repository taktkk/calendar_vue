<script setup>
import Calendar from './components/Calendar.vue';
import { ref , reactive, computed , onMounted} from "vue" 

</script>

<template>
  
  <Calendar/>
  
</template>


<style>
body{
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #fdf6e3;

}
</style>


