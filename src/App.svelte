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

	const deleteTodo = (e) => {
		let id = e.detail;	
		todos = todos.filter((x) => x.id !== id);
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
	<TodoList {todos} on:deleteTodo={deleteTodo} />
</main>
