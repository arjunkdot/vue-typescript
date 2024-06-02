<script lang="ts">
import { defineComponent, type PropType, computed } from 'vue'
import { type Job } from '../types/job'
import { type OrderTerm } from './../types/orderTerm'
export default defineComponent({
  name: 'JobList',
  props: {
    jobs: {
      type: Array as PropType<Job[]>,
      required: true
    },
    order: {
      type: String as PropType<OrderTerm>,
      required: true
    }
  },
  setup(props) {
    const orderedJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] > b[props.order] ? 1 : -1
      })
    })

    return {
      orderedJobs
    }
  }
})
</script>
<template>
  <div class="job-list">
    <p>Ordered by {{ order }}</p>
    <ul>
      <transition-group name="list" tag="ul">
        <li v-for="job in orderedJobs" :key="job.id">
          <h2>{{ job.title }} in {{ job.location }}</h2>
          <div class="salary">
            <img src="./../assets/rupee.svg" alt="Rupee" />
            <p>{{ job.salary }} rupees</p>
          </div>
          <div class="description">
            Lorem, ipsum dolor sit amet consectetur adipisicing elit. Itaque, maxime repellat nemo
            quis odio deleniti blanditiis, adipisci atque modi consequatur fugit autem illo iste
            iure in, error ea dolores officia?
          </div>
        </li>
      </transition-group>
    </ul>
  </div>
</template>
<style scoped>
.job-list {
  max-width: 960px;
  margin: 40px auto;
}
.job-list ul {
  padding: 0;
}
.job-list li {
  list-style-type: none;
  background: white;
  padding: 16px;
  margin: 16px 0;
  border-radius: 4px;
}
.job-list h2 {
  margin: 0 0 10px;
  text-transform: capitalize;
}
.salary {
  display: flex;
}
.salary img {
  width: 30px;
}
.salary p {
  color: #17bf66;
  font-weight: bold;
  margin: 10px 4px;
}
.list-move {
  transition: all 0.2s linear;
}
</style>
