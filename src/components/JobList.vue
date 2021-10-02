<template>
	<div class="job-list">
    <p>Ordered by {{order}}</p>
		<ul>
			<li :key="job.id" v-for="job in orderedJobs">
				<h2>{{ job.title }} - {{ job.location }}</h2>
				<div class="salary">
					<p>{{ job.salary }} rupees</p>
				</div>
				<div class="description">
					<p>
						Lorem ipsum dolor sit amet consectetur adipisicing elit. Nemo
						commodi illum optio aliquid, neque ut laborum amet nisi vel
						sapiente?
					</p>
				</div>
			</li>
		</ul>
	</div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from "vue";
import Job from "@/types/Job";
import OrderTerm from "@/types/OrderTerm";

export default defineComponent({
	props: {
		jobs: {
			required: true,
			type: Array as PropType<Job[]>,
		},
    order: {
      required: true,
      type: String as PropType<OrderTerm>
    }
	},
  setup(props) {
    //in order to access the jobs we need to pass the props into setup
    const orderedJobs = computed(() => {
    //sort will fire a function for each consecutive pair of elements inside the array (a,b)
    //if we return -1 for this pair then the order of that pair will remain the same
    //if we return +1 it switches the order, we will do this to all items in our array until it matches our criteria
      return [...props.jobs].sort((a: Job, b: Job) => {
        //we are comparing the order property of a & b
        //if a is bigger than b we want to return +1
        return a[props.order] > b[props.order] ? 1 : -1
      })
    })
    return { orderedJobs }
  },
});
</script>

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
</style>
