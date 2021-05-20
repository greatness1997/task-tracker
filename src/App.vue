<template>
	<div class="container">
		<div id="app">
			<Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask"/>
			<div v-show="showAddTask">
				<AddTask @add-task="addTask"/>
			</div>
			<Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
		</div>
	</div>
</template>

<script>
	import Header from "./components/header.vue";
	import Tasks from "./components/Tasks.vue";
	import AddTask from "./components/AddTask.vue";
	export default {
		name: "App",
		components: {
			Header,
			Tasks,
			AddTask
		},
		data() {
			return {
				tasks: [],
				showAddTask: false,
			};
		},
		methods: {
			toggleAddTask(){
				this.showAddTask = !this.showAddTask
			},
			addTask(task){
				this.tasks = [...this. tasks, task]
			},
			deleteTask(id) {
				if (confirm("Are You Sure?")) {
					this.tasks = this.tasks.filter(task => task.id !== id);
				}
			},
			toggleReminder(id) {
				this.tasks = this.tasks.map(task =>
					task.id === id ? { ...task, reminder: !task.reminder } : task
				);
			}
		},
		created() {
			this.tasks = [
				{
					id: 1,
					text: "Doctor appointment",
					day: "March 1st at 12:30pm",
					reminder: true
				},
				{
					id: 2,
					text: "meeting at school",
					day: "March 3rd at 1:30pm",
					reminder: true
				},
				{
					id: 3,
					text: "Food Shopping",
					day: "March 3rd at 11:30pm",
					reminder: false
				}
			];
		}
	};
</script>

<style>
	@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=wrap");
	* {
		box-sizing: border-box;
		margin: 0;
		padding: 0;
	}

	body {
		font-family: "Poppins", sans-serif;
	}

	.container {
		max-width: 500px;
		margin: 30px auto;
		overflow: auto;
		min-height: 300px;
		border: 1px solid steelblue;
		padding: 30px;
		border-radius: 5px;
	}
	.btn {
		cursor: pointer;
		display: inline-block;
		background: #000;
		color: white;
		font-size: 15px;
		border: none;
		padding: 10px 20px;
		margin: 5px;
		text-decoration: none;
		font-family: inherit;
	}

	.btn:focus {
		outline: none;
	}

	.btn:active {
		transform: scale(0.98);
	}

	.btn-block {
		display: block;
		width: 100%;
	}
</style>
