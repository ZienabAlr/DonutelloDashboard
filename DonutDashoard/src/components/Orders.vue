<script setup>
import { ref } from 'vue'

</script>

<template>

<div class="order">
    <img src="../assets/donutTestimg.jpeg" alt="">
    <h3>Donut name</h3>
    <p class="client"> Client name</p>
    <p class="status">status: </p>
    <!-- detail button  -->
    <button class=" details">Details</button>
    <!-- delete button  -->
    <button class="delete">Delete</button>
  
</div>

</template>

<style scoped>
.order {
   
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    padding: 0.5rem;
    margin: 5rem 1rem;
    border-radius: 0.5rem;
    width: 200px;
    height: 300px;
    background: #fff;
    
}
/* center order img */
.order img {
    display: block;
    margin-left: auto;
    margin-right: auto;
    width: 100px;
    height: 100px;
    border-radius: 50%;
    
}


</style>