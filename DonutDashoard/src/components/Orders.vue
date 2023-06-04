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

.order h3 {
    text-align: center;
    font-size: 1.5rem;
    margin: 0.5rem 0;
    color: #333;
}

.order p {
    margin: 1rem;  
}
.order .client {
    font-size: 1rem;
    color: rgb(143, 143, 143);
    text-align: center;
    font-weight: 200;

}
.order .status {
    font-weight: 700;
}

.order button {
display: inline-block;
margin: 0.5rem 0.75rem;
padding:  0.75rem 1rem;
border: none;
border-radius: 0.25rem;
font-size: 14px;
box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
}
.order .details {
background: #E72770;
color: #fff;
}
.order .details:hover {
background: #e72771ae;
color: #fff;
}
.order .delete {
background: rgba(255, 255, 255, 0);
color: #e7274a;
border: 1px solid #e72727;
}
</style>