<script setup>
import carsData from '../data.json'
import { ref, watch, onMounted } from 'vue'
import { useRouter, useRoute } from 'vue-router'

const router = useRouter()
const route = useRoute()

const cars = ref(carsData)
const make = ref("")

onMounted(() => {
  make.value = route.query.make || ""
})

watch(make, () => {
  if (make.value) {
    if (make.value === "All") cars.value = carsData;
    else {
      cars.value = carsData.filter(c => c.make === make.value)
    }
  }
})

const handleChange = () => {
  router.push({query: {make: make.value}})
}
</script>

<template>
  <main class="container">
    <h1>Our Cars</h1>
    <select @change="handleChange" v-model="make" class="select">
      <option value="All" selected>All</option>
      <option value="Chevrolet">Chevrolet</option>
      <option value="Porsche">Porsche</option>
      <option value="Audi">Audi</option>
    </select>
    <div class="cards">
      <div
        v-for="car in cars"
        :key="car.id"
        class="card"
        @click="router.push(`/car/${car.id}`)"
      >
        <h1>{{ car.make }}</h1>
        <p>${{ car.price }}</p>
      </div>
    </div>
  </main>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.select {
  margin-top: 20px;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
  outline: none;
  transition: border-color 0.3s ease-in-out;
}

.select:focus {
  border-color: #888;
}

.cards {
  display: flex;
  width: 1000px;
  flex-wrap: wrap;
  margin-top: 50px;
  justify-content: center;
  animation: fade-in 0.5s ease-in-out;
}

.card {
  box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.207);
  padding: 15px;
  width: 150px;
  margin-right: 15px;
  cursor: pointer;
  margin-bottom: 20px;
  transition: transform 0.3s ease-in-out;
}

.card:hover {
  transform: translateY(-5px);
}

@keyframes fade-in {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
