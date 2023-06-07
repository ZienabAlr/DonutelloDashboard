<script setup>
import { onMounted, ref, reactive } from 'vue'

let orders = reactive({data: []}); 
let company = ref('');
let email = ref('');
let phone = ref('');
let donutname = ref('');
let glaze = ref('');
let amount = ref('');
let status = ref('');
onMounted(()=>{
    const url = 'http://localhost:3000/api/v1/donutello';

    fetch(url)
    .then((respons) => respons.json())
    .then((data) => {
        orders.data = data.data.donuts;
    })
})

// delete order function
const deleteOrder = (id) => {
    const url = `http://localhost:3000/api/v1/donutello/${id}`;
    fetch(url, {
        method: 'DELETE',
    })
    .then((response) => response.json())
    .then((data) => {
        // get the index of the item
        const index = data.data.donut._id;
        orders.data.splice(index, 1);
    })
    .catch((error) => {
        console.log(error);
    })
}

const getOneOrder = (id) => {
    const url = `http://localhost:3000/api/v1/donutello/${id}`;
    fetch(url)
    .then((response) => response.json())
    .then((data) => {
        const order = data.data.donut;
        company.value = order.company;
        email.value = order.email;
        phone.value = order.phone;
        donutname.value = order.donutname;
        glaze.value = order.glaze;
        amount.value = order.amount;
        status.value = order.status;

        // show the pop up card
        window.location.href = "#popup1";
    })
    .catch((error) => {
        console.log(error);
    })
}

// update order function

const updateOrder = (id) => {
    const update = {
        status: status.value
    }
    const url = `http://localhost:3000/api/v1/donutello/${id}`;
    fetch(url, {
        method: 'PUT',
        headers: {
            'Content-Type': 'application/json',
        },
        body: JSON.stringify(update),
    })
    .then((response) => response.json())
    .then((data) => {
        
        status.value = order.status;

        // show the pop up card
        window.location.href = "#popup1";
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
    <p class="status">status: <span>{{item.status }} </span></p>
    <button class=" details" @click.prevent="getOneOrder(item._id)">Details</button>
    <button class="delete" @click.prevent="deleteOrder(item._id)">Delete</button>
</div>

<!-- make a pop up card with information of one order -->
    <div id="popup1" class="overlay">
    <div class="popup">
        <h2>{{donutname}}</h2>
        <a class="close" href="#">&times;</a>
        <div class="content">
            <p>Bedrijfsnaam: <span>{{company}}</span></p>
            <p>E-mail: <span>{{email}}</span></p>
            <p>Gsm nummer: <span>{{phone}}</span> </p>
            <p>Glazuur: <span>{{glaze}}</span></p>
            <p>Aantal: <span> {{amount}}</span></p>
            <p>Status: 
                <select v-model="status">
                    <option disabled value=""></option>
                    <option>To Do</option>
                    <option>In verwerking</option>
                    <option>Klaar</option>
                </select>
            </p>
        </div>
        <button class="details update" @click.prevent="updateOrder(orderId)">Update</button>
    </div>
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
.order .status span {
    color: #e72727;
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
.details {
background: #E72770;
color: #fff;
}
.details:hover {
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

.overlay {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.7);
  transition: opacity 500ms;
  visibility: hidden;
  opacity: 0;
}
.overlay:target {
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
  color: #E72770;
  text-align: center;
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
}
.content p {
    font-size: 1rem;
    margin: 0.5rem 1rem;
    color: #333;
    font-weight: 700;
}
.content p span {
    font-weight: 200;
}
.content p select {
    padding:  0.5rem 0;
    border: 1px solid #1eb121;
    border-radius: 0.25rem;
    margin: 0.5rem 0;
}

.update {
   border: none;
    border-radius: 0.25rem;
    padding: 0.85rem 1rem;
    position: absolute;
    bottom: 7px;
    right: 0;
    margin: 0.5rem 1rem;

}
</style>