<template>
	<div>
		<div @dblclick="$emit('toggle-reminder', task.id)" :class="[task.reminder ? 'reminder' : '', 'task']">
			<h3>
				{{ task.text }}
				<h6 @click="$emit('delete-task', task.id)" class="delete">Del</h6>
			</h3>
			<p>{{ task.day }}</p>
		</div>
	</div>
</template>

<script>
	export default {
		name: "Task",
		props: {
			task: Object
		},
	};
</script>
 
<style scope>
	.task h6 {
		color: red;
		font-weight: bold;
	}
	.task {
		background: #f4f4f4;
		margin: 5px;
		padding: 10px 20px;
		cursor: pointer;
	}
	.task.reminder {
		border-left: 5px solid green;
	}

	.task h3 {
		display: flex;
		align-items: center;
		justify-content: space-between;
	}
</style>