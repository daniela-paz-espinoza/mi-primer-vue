<script setup>
import { computed, ref } from 'vue';


const saludo = ("Vue Dinamico")
const counter = ref(0)
const arrayFavoritos = ref([])

const increment = () => {
  counter.value++;

}

const disminuir = () => {
  counter.value--;

}

const resetear = () => {
  (counter.value = 0);

}

const agregar = () => {
  arrayFavoritos.value.push(counter.value)
}

const bloquearBtnAgregar = computed(() => {
  const numSearch = arrayFavoritos.value.find(num => num === counter.value)
  if (numSearch === 0) return true

  return numSearch ? true : false
})

const classCounter = computed(() => {
  if (counter.value === 0) {
    return 'zero'
  }
  if (counter.value > 0) {
    return 'positive'
  } if (counter.value < 0) {
    return 'negative'
  }
})

//Pinta el contador en rojo cuando el valor sea menor a cero.

//Pinta el contador en verde cuando el valor sea mayor a cero.

</script>

<template>
  <div class="container text-center mt-3">
    <h1>Hola! {{ saludo }}</h1>
    <h2 :class="classCounter">{{ counter }}</h2>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Aumentar</button>
      <button @click="disminuir" class="btn btn-danger">Disminuir</button>
      <button @click="resetear" class="btn btn-secondary">Resetear</button>
      <button @click="agregar" :disabled="bloquearBtnAgregar" class="btn btn-primary">Agregar</button>
    </div>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="(num, index) in arrayFavoritos" :key="index">
        {{ num }}
      </li>
    </ul>
  </div>
</template>

<style>
h1 {
  color: red;
}

.negative {
  color: red;
}

.positive {
  color: green;
}

.zero {
  color: blue;
}
</style>
