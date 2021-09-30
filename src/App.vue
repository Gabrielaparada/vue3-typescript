<template>
<div class="app">
  <p> {{jobs[0].location}}</p>
</div>
</template>

<script lang="ts">
import Job from './types/Job'
import { defineComponent, reactive, toRefs, ref } from 'vue';

export default defineComponent({
  name: 'App',
  components: {
    
  },
  //Composition API
  setup() {
    //every job that is loaded here must follow the interface 'Job' structure
    const jobs = ref<Job[]>([
      {title: 'Farm worker', location: 'lon lon ranch', salary: 30000, id: '1'},
      {title: 'Cleaner', location: 'Toronto', salary: 40000, id: '2'},
      {title: 'Gardener', location: 'Strawberry Fields', salary: 38000, id: '3'},
      {title: 'Painter', location: 'Hamilton', salary: 30000, id: '4'},
      {title: 'Dancer', location: 'School of dance', salary: 50000, id: '5'}
    ])
    return { jobs }
  },
  //Options API
  // data() {
  //   return {
  //     name: 'Link',
  //     //type casting
  //     age: 25 as number | string
  //   }
  // },
  methods: {

  }
});
</script>

<style>

</style>
