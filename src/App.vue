<template>
	<div class="app">
    <header>
      <h1> Job board </h1>
      <div class="order">
        <button @click="handleClick('title')"> Order by title</button>
        <button @click="handleClick('salary')"> Order by salary </button>
        <button @click="handleClick('location')"> Order by location</button>
      </div>
    </header>
		<JobList :jobs="jobs" :order="order" />
	</div>
</template>

<script lang="ts">
import Job from "./types/Job";
import { defineComponent, reactive, toRefs, ref } from "vue";
import JobList from "./components/JobList.vue";
import OrderTerm from './types/OrderTerm'
export default defineComponent({
	name: "App",
	components: {
		JobList,
	},
	//Composition API
	setup() {
		//every job that is loaded here must follow the interface 'Job' structure
		const jobs = ref<Job[]>([
			{
				title: "Farm worker",
				location: "lon lon ranch",
				salary: 30000,
				id: "1",
			},
			{ title: "Cleaner", location: "Toronto", salary: 40000, id: "2" },
			{
				title: "Gardener",
				location: "Strawberry Fields",
				salary: 38000,
				id: "3",
			},
			{ title: "Painter", location: "Hamilton", salary: 30000, id: "4" },
			{ title: "Dancer", location: "School of dance", salary: 50000, id: "5" },
		]);
    // we are creating local state using a ref to keep track of the OrderTerm, initially it will be 'title'
    //but it can change to be 'location' or 'salary' as stated in OrderTerm
    const order = ref<OrderTerm>('title')
    //passing OrderTerm as an argument to make sure we only accept the specific info we need title, location or salary.
    const handleClick = (term: OrderTerm) => {
      order.value = term
    }
		return { jobs, handleClick, order };
	},
	//Options API
	// data() {
	//   return {
	//     name: 'Link',
	//     //type casting
	//     age: 25 as number | string
	//   }
	// },
	methods: {},
});
</script>

<style>
  header {
    text-align: center;
  }
  header .order {
    margin-top: 20px;
  }
  button {
    margin: 0 10px;
    color: white;
    background: forestgreen;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    border: 1px solid darkgray;
  }
</style>
