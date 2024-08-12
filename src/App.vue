

<template>
  <header class="bg-blue-950 text-white px-3 py-4 mb-6">
    <h1 class="text-xl font-semibold">
      Benevolent<sup class="text-[0.5rem] top-[-0.5rem] ml-[1px]">AI</sup>
    </h1>
  </header>

  <main class="w-full max-w-screen-lg mx-auto px-3 grow">
    <section>
      <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-8" v-if="!isLoading">
        <Article v-for="item in resultCollection" :key="item.targetId" :item="item" />
      </div>

      <p v-else>&hellip;Loading</p>
    </section>
  </main>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import Article from './components/Article.vue'

const API_URL = 'https://api.jsonbin.io/v3/'
const endpoint = 'b/633c651b0e6a79321e1ce138'

const isLoading = ref(true)
const resultCollection = ref([])

onMounted(async () => {
  try {
    const response = await fetch(`${API_URL}${endpoint}`)
    const data = await response.json()
    resultCollection.value = data?.record?.targets
  }
  catch(error) {
    console.log('An error occured trying to retrieve the data')
  }
  finally {
    isLoading.value = false
  }
})
</script>
