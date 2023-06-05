<script setup>
import { onMounted, ref, reactive } from 'vue'

let orders = reactive({data: []}); 

onMounted(()=>{
    const url = 'http://localhost:3000/api/v1/donutello';

    fetch(url)
    .then((respons) => respons.json())
    .then((data) => {
        orders.data = data.data.donuts;
        // console.log(data);
    })
})

// delete one order
const deleteOrder = (id) => {
    const url = `http://localhost:3000/api/v1/donutello/${id}`;
    fetch(url, {
        method: 'DELETE',
    })
    .then((respons) => respons.json())
    .then((data) => {
        console.log(data);
         orders.data = data.data.donuts[this.id];

    })
    .catch((error) => {
        console.log(error);
    })
}
</script>

<template>

<div v-for="item in orders.data" :key="item" class="order" >
    <img src="../assets/donutTestimg.jpeg" alt="">
    <h3>{{item.donutname}}</h3>
    <p class="client"> {{ item.company }}</p>
    <p class="status">status: {{item.status }} </p>
    <!-- detail button  -->
    <button class=" details">Details</button>
    <!-- delete button  -->
    <button class="delete" @click.prevent="deleteOrder">Delete</button>
  
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
    display: inline-block;
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
.order .delete:hover {
background: #e72727;
color: #fff;
}

/* .overlay {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.7);
  transition: opacity 500ms;
  visibility: hidden;
  opacity: 0;
} */
/* .overlay:target {
  visibility: visible;
  opacity: 1;
}

.popup {
  margin: 70px auto;
  padding: 20px;
  background: #fff;
  border-radius: 5px;
  width: 30%;
  position: relative;
  transition: all 5s ease-in-out;
}

.popup h2 {
  margin-top: 0;
  color: #333;
  font-family: Tahoma, Arial, sans-serif;
}
.popup .close {
  position: absolute;
  top: 20px;
  right: 30px;
  transition: all 200ms;
  font-size: 30px;
  font-weight: bold;
  text-decoration: none;
  color: #333;
}
.popup .close:hover {
  color: #06D85F;
}
.popup .content {
  max-height: 30%;
  overflow: auto;
} */

</style>