<script lang="ts">
import { defineComponent, reactive, ref, toRefs } from 'vue'
import type { Job } from './types/Job'
import type { OrderTerm } from './types/OrderTerm'
import JobList from './components/JobList.vue'

export default defineComponent({
  name: 'App',
  components: { JobList },
  setup() {
    // const state = reactive({
    //   name: 'Link',
    //   age: 25 as number | string,
    // })
    // state.name = 'Shaun'
    // state.age = '26'
    // return { ...toRefs(state) }
    // const name = ref('Link')
    // const age = ref<number | string>(25)
    // return { name, age }

    const jobs = ref<Job[]>([
      { title: 'farm worker', location: 'lon lon ranch', salary: 30000, id: '1' },
      { title: 'quarryman', location: 'death mountain', salary: 40000, id: '2' },
      { title: 'flute player', location: 'the lost woods', salary: 35000, id: '3' },
      { title: 'fisherman', location: 'lake hylia', salary: 21000, id: '4' },
      { title: 'prison guard', location: 'gerudo valley', salary: 32000, id: '5' },
    ])
    const order = ref<OrderTerm>('title')

    const handleClick = (term: OrderTerm) => {
      order.value = term
    }

    return { jobs, handleClick, order }
  },
  // methods: {
  //   changeName(name: string) {
  //     this.name = name
  //     return name
  //   },
  //   changeAge(age: number | string) {
  //     this.age = age
  //     return age
  //   },
  // },
})
</script>

<template>
  <div class="app">
    <!-- <p>{{ name }} - {{ age }}</p>
    <button @click="changeName('Zelda')">change name</button>
    <button @click="changeAge(30)">change age</button> -->
    <header class="text-center">
      <div class="title flex justify-center items-center">
        <img src="./assets/heart.svg" alt="site logo" class="w-15 mr-5" />
        <h1 class="text-5xl font-[HyliaSerif] tracking-tight my-10">Hyrule Jobs</h1>
      </div>
      <div
        class="order mt-5 [&>button]:mx-3 [&>button]:text-main [&>button]:bg-surface [&>button]:border-main [&>button]:cursor-pointer [&>button]:border-4 [&>button]:px-4 [&>button]:py-2 [&>button]:rounded-md [&>button]:font-bold [&>button]:active:bg-main [&>button]:active:text-surface"
      >
        <button @click="handleClick('title')">order by title</button>
        <button @click="handleClick('salary')">order by salary</button>
        <button @click="handleClick('location')">order by location</button>
      </div>
    </header>
    <JobList :jobs="jobs" :order="order" />
  </div>
</template>

<style scoped></style>
