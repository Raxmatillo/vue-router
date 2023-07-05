<script setup>
import {useRoute, useRouter, RouterView} from 'vue-router'
import {ref, onBeforeMount} from "vue"
import cars from "../data.json"


const car = ref(null)
const route = useRoute()
const router = useRouter()
const {id} = route.params

onBeforeMount(() => {
    car.value = cars.find(c => c.id === parseInt(id))
})


</script>


<template>
    <div class="container">
        <div class="car-details" v-if="car">
            <p><span class="label">Make:</span> {{ car.make }}</p>
            <p><span class="label">Body:</span> {{ car.body }}</p>
            <p><span class="label">Price:</span> {{ car.price }}</p>
            <p><span class="label">Year:</span> {{ car.year }}</p>
            <button class="go-back-button" @click="router.back">Go back</button>
            <RouterView/>
        </div>
        <div v-else>
            <h1 class="not-found-message">Car Not Found</h1>
        </div>
    </div>
</template>


<style scoped>
.container {
    margin: 20px;
    padding: 20px;
    background-color: #f5f5f5;
    border: 1px solid #ddd;
    border-radius: 6px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.title {
    color: #333;
    font-size: 24px;
    font-weight: 600;
    margin-bottom: 20px;
}

.car-details {
    background-color: #333;
    padding: 20px;
    border-radius: 4px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.label {
    font-weight: bold;
    margin-right: 10px;
}

p {
    margin-bottom: 10px;
    font-size: 18px;
    line-height: 1.4;
}

.go-back-button {
    background-color: #ddd;
    border: none;
    padding: 8px 12px;
    border-radius: 4px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s ease-in-out;
}

.go-back-button:hover {
    background-color: #ccc;
}

.not-found-message {
    color: #333;
    font-size: 24px;
    margin-bottom: 20px;
}


</style>