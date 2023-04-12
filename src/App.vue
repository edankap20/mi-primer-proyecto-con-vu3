<script setup>
import {ref, computed} from 'vue'

const name = 'Vue Dinámico'

const counter = ref(0);
const listaFavoritos = ref([])
const increment = () => counter.value++;
const decrement = () => counter.value --;
const reset = () => counter.value = 0;

const bloquearBotonAdd = computed(() => {
  const busquedaNumero = listaFavoritos.value.find(numero => numero === counter.value)
  if (busquedaNumero === 0 ) return true
  return busquedaNumero ? true : false
})

const add = () => {
  listaFavoritos.value.push(counter.value)
}
const classCounter = computed(() => {
  if (counter.value === 0) {
    return 'zero'
  }

  if (counter.value > 0 ){
    return 'positive'
  }

  if (counter.value < 0) {
    return 'negative'
  }
});
</script>

<template>
  <div class="container text-center mt-3">
      <h1>{{name.toUpperCase()}}</h1>
      <h2 :class="classCounter">{{ counter }}</h2>
      <div class="btn-group">
        <button @click="increment" class="btn btn-success">Aumentar</button>
        <button @click="decrement" class="btn btn-danger">Disminuir</button>
        <button @click="reset" class="btn btn-secondary">Resetear</button>
        <button @click="add" :disabled="bloquearBotonAdd" class="btn btn-primary">Añadir número favorito</button>
      </div>
      <ul class="list-group mt-4">
        <li
          class="list-group-item"
          v-for="(numero, index) in listaFavoritos"
          :key="index"
        >
        {{ numero }}
        </li>
      </ul>
  </div>

</template>


<style>
h1 {
  color: red;
}
.positive {
  color: green
}
.negative {
  color: red
}
.zero {
  color: peru
}
</style>