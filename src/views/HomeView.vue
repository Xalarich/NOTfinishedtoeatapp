<script setup lang="ts">
import { ref } from "@vue/reactivity"

enum RestaurantStatus {
  Recommended = 'Recommended',
  WantToTry = 'Want To Try',
  MustTry = 'Must Try'
} 

interface Restaurant {
  name?: string
  address?: string
  status?: RestaurantStatus
  dishes?: Dish[]
}

// type RestaurantStatus = 'Want to try' | 'Recommended' | 'Do Not Recommend' | 'Must Try'

const restaurantList = ref<Restaurant[]>([]);
const newRestaurant = ref<Restaurant>({});

// const statusList = [
//   'Want to Try',
//   'Recommended',
//   'Do Not Recommend',
//   'Must Try'
// ]

function addRestaurant() {
  restaurantList.value.push({
  name: newRestaurant.value.name,
  address: '',
  status: 'Want to Try',
  dishes: []
})
}
</script>

<template>
  <main>
    <pre>
      {{ newRestaurant }}
    </pre>
    <form @submit.prevent="addRestaurant">
      <div>
        <label for="restaurant-name">Restaurant Name</label>
        <input 
          type="text" 
          id="restaurant-name" 
          v-model="newRestaurant.name">
      </div>
      <div>
        <label for="restaurant-address">Restaurant Address</label>
        <input 
          type="text" 
          id="restaurant-address"
          v-model="newRestaurant.address"
        />
      </div>
      <div>
        <label for="restaurant-status">Restaurant Status</label>
        <select 
        name="restaurant-status" 
        id="restaurant-status"
        v-model="newRestaurant.status"
        >
          <option v-for="status in statusList" :value="status" :key="status" >
            {{ status }}
          </option>
        </select>
      </div>
      <button type="submit">Add Restaurant</button>
    </form>
    <ul>
      <li v-for="restaurant in restaurantList" :key="restaurant.name">
        {{ restaurant.name }}
      </li>
    </ul>
  </main>
</template>
