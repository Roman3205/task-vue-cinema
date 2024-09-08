<script setup>
import { ref } from "vue";
import { items } from "./movies.json";
/*
 This is an Icon that you can use to represent the stars if you like
 otherwise you could just use a simple ⭐️ emoji, or * character.
*/
import { StarIcon } from "@heroicons/vue/24/solid";
const movies = ref(items);
const updateRating = (itemIndex, star) => {
  console.log(itemIndex);
  movies.value[itemIndex].rating = star;
};
</script>

<template>
  <!-- This is where your template goes	-->
  <div class="flex justify-center gap-10 flex-wrap">
    <div
      v-for="(item, itemIndex) in movies"
      :key="item.id"
      class="max-w-[300px] h-auto bg-black"
    >
      <div class="relative w-full h-2/3">
        <img class="w-full h-full" :src="item.image" :alt="item.name" />
        <div v-if="item.rating" class="absolute top-2 right-2">
          <StarIcon class="w-12 relative h-12 text-yellow-500"></StarIcon>
          <span
            class="absolute top-2.5 bottom-0 right-1/3 pr-1 font-semibold text-yellow-700 text-lg"
            >{{ item.rating }}</span
          >
        </div>
      </div>
      <div class="p-3 bg-white w-full h-1/3 rounded-b-lg text-xs flex flex-col">
        <div class="flex flex-col gap-2 flex-1">
          <h1 class="font-bold text-lg">{{ item.name }}</h1>
          <div class="flex gap-2">
            <div
              class="rounded-lg bg-indigo-500 text-white p-1.5"
              v-for="genre in item.genres"
              :key="genre"
            >
              {{ genre }}
            </div>
          </div>
          <p>{{ item.description }}</p>
        </div>
        <div class="flex gap-2 pb-2">
          <span>Rating ({{ item.rating }}/5)</span>
          <div class="flex gap-0">
            <button
              class="w-4 h-4"
              v-for="index in 5"
              :key="index"
              :disabled="index === item.rating"
              @click="updateRating(itemIndex, index)"
              :class="
                index <= item.rating ? 'text-yellow-500' : 'text-gray-500'
              "
            >
              <StarIcon></StarIcon>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
