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
