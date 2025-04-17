<script lang="ts">
import type { Job } from '@/types/Job'
import type { OrderTerm } from '@/types/OrderTerm'
import { computed, defineComponent, type PropType } from 'vue'

export default defineComponent({
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>,
    },
    order: {
      required: true,
      type: String as PropType<OrderTerm>,
    },
  },
  setup(props) {
    const orderedJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] > b[props.order] ? 1 : -1
      })
    })

    return { orderedJobs }
  },
})
</script>

<template>
  <div class="job-list max-w-240 my-10 mx-auto">
    <p class="my-4">Ordered by {{ order }}</p>
    <TransitionGroup
      name="list"
      tag="ul"
      moveClass="transition-all duration-1000"
      class="flex flex-col gap-y-4"
    >
      <li class="list-none bg-white p-4 rounded-sm" v-for="job in orderedJobs" :key="job.id">
        <h2 class="capitalize mb-3 text-2xl font-bold">{{ job.title }} in {{ job.location }}</h2>
        <div class="salary flex [&>p]:text-highlight [&>p]:font-bold [&>p]:my-3 [&>p]:mx-1">
          <img src="../assets/rupee.svg" alt="rupee icon" class="w-8" />
          <p>{{ job.salary }} rupees</p>
        </div>
        <div class="description">
          <p>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin arcu purus, finibus a
            pulvinar nec, dignissim nec mauris. Maecenas massa mauris, molestie nec porttitor et,
            mattis eget erat. Ut sit.
          </p>
        </div>
      </li>
    </TransitionGroup>
  </div>
</template>

<style></style>
