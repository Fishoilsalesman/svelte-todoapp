<script>
	import AddTodoForm from "./components/AddTodo.svelte";
	import TodoList from "./components/TodoList.svelte";

	let todos = [
		{
			id: 1,
			todo: "Clean room",
			due: "2020-10-8",
		},
	];

	const addTodo = (e) => {
		let newTodo = e.detail;
		todos = [newTodo, ...todos];
	};
</script>

<style>
	main {
		max-width: 600px;
		margin: 0 auto;
	}
</style>

<AddTodoForm on:addTodo={addTodo} />
<main>
	<TodoList {todos} />
</main>
