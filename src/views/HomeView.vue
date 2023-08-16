<script setup lang="ts">
import { ref } from 'vue'

/**
 * Restaurant
 *
 * Name - string
 * Adress - string
 * Rating - number
 * Status - string ("want to try" | "must try")
 * Dishes - array of Dish objects
 */

interface Restaurant {
  name?: string
  rating?: number
  status?: keyof typeof recommendStatus
  dishes?: Dish[]
}

interface Dish {
  name: string
  diet?: Diet
  status?: keyof typeof recommendStatus
}

type Diet = 'vegeterian' | 'vegan' | 'gluten-free'

// type RestaurantStatus = 'Want to try' | 'Recommended' | 'Do not recommend' | 'Must try'

enum recommendStatus {
  WantToTry = 'Want to try',
  Recommended = 'Recommended',
  DoNotRecommend = 'Do not recommend',
  MustTry = 'Must try'
}

const restaurantList = ref<Restaurant[]>([])
const newRestaurant = ref<Restaurant>({
  status: 'WantToTry'
})

// how to extract value from types
// const statusList = ['Want to try', 'Recommended', 'Do not recommend', 'Must try']

function addRestaurant() {
  restaurantList.value.push({
    name: newRestaurant.value.name,
    rating: newRestaurant.value.rating,
    status: newRestaurant.value.status,
    dishes: []
  })
}
</script>

<template>
  <pre> {{ newRestaurant }}</pre>
  <main>
    <!-- Create a form allows user to add a restaurant to a list  -->
    <form @submit.prevent="addRestaurant">
      <div>
        <label for="restaurant-name">Restaurant Name</label>
        <input type="text" id="restaurant-name" v-model="newRestaurant.name" />
      </div>
      <div>
        <label for="restaurant-rating">Restaurant rating</label>
        <input type="text" id="restaurant-rating" v-model="newRestaurant.rating" />
      </div>
      <div>
        <label for="restaurant-dishes">Restaurant dishes</label>
        <input type="text" id="restaurant-dishes" v-model="newRestaurant.dishes" />
      </div>
      <div>
        <label for="restaurant-status">Restaurant status</label>
        <select id="restaurant-status" v-model="newRestaurant.status">
          <option v-for="status in Object.values(recommendStatus)" :key="status" :value="status">
            {{ status }}
          </option>
        </select>
      </div>
      <button type="submit">Add Restaurant</button>
    </form>
    <ul>
      <li v-for="restaurant in restaurantList" :key="restaurant.name">
        {{ restaurant.name }} - {{ restaurant.status }}
      </li>
    </ul>
  </main>
</template>
