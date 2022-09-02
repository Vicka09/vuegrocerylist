<script setup>
  import { ref } from 'vue'
  import {useStorage} from '@vueuse/core'
  import {nanoid} from 'nanoid'
  import confetti from 'canvas-confetti'

  const newGrocery = ref('')
  const groceries = useStorage('groceries',[])

  const addGrocery = () => {
    if(newGrocery.value){
    groceries.value.push({id:nanoid(), name: newGrocery.value})
    newGrocery.value = ''
  }
}

const deleteGrocery = id => {
  const removeIndex = groceries.value.findIndex(grocery => grocery.id === id)
  groceries.value.splice(removeIndex, 1)
    confetti({ particleCount: 500, spread: 500, origin: { y: 1 } })
} 

</script>

<template>
<main>
  <h1 class = "title"> Vue Grocery List 📝✏️</h1>
  <form class = "newGroceryForm" @submit.prevent="addGrocery">
      <input id = "newGrocery"
      autocomplete ="off"
      type = "text"
      placeholder = "Add item to the list"
      v-model="newGrocery"
      />
      <button id = "addBtn" type="submit">Add</button>
  </form>
  <h2> Pending Items: {{groceries.length}}</h2>
  <ul>
    <li v-for="grocery in groceries" @click="deleteGrocery(grocery.id)">
        {{ grocery.name }}
      </li>
  </ul>
</main>
</template>

<style lang="postcss" scoped>
  main {
    @apply mt-8 flex flex-col justify-center items-center gap-8;
    .title {
      @apply m-2 text-6xl font-light tracking-wider text-accent;
    }
    form {
      @apply flex focus-within:ring-8 focus-within:ring-accent focus-within:rounded-lg;
      input {
        @apply bg-white text-comment p-2 w-80 text-2xl rounded-l-md outline-none;
      }
      button {
        @apply bg-accent text-background p-2 text-2xl font-bold rounded-r-md;
        &:hover {
          @apply bg-bluish;
        }
      }
    }
    ul {
      @apply flex flex-col items-center justify-center rounded-lg bg-greenish;
      li {
        @apply bg-white text-black m-2 p-2 w-96 text-center;
        &:hover {
          @apply bg-accent font-bold cursor-pointer;
        }
      }
    }
  }
</style>
