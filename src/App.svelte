<script>
	import { onMount } from "svelte";
	import AddTodoForm from "./components/AddTodo.svelte";
	import TodoList from "./components/TodoList.svelte";
	import Modal from "./components/Modal.svelte";
	import EditForm from "./components/EditForm.svelte";

	let showModal = false;
	let selectedTodo = {};

	let todos = [];

	onMount(async () => {
		todos = JSON.parse(localStorage.getItem("todos"));
	});

	const saveTodos = () => {
		localStorage.setItem("todos", JSON.stringify(todos));
	};

	const toggleModal = () => {
		showModal = !showModal;
	};

	const addTodo = (e) => {
		let newTodo = e.detail;
		todos = [newTodo, ...todos];
		saveTodos();
	};

	const deleteTodo = (e) => {
		let id = e.detail;
		todos = todos.filter((x) => x.id !== id);
		saveTodos();
	};

	const editTodo = (e) => {
		showModal = !showModal;

		let { id } = e.detail;
		selectedTodo = todos.find((x) => x.id == id);
	};
	const handleUpdateTodo = (e) => {
		let updatedTodo = e.detail;

		let objIndex = todos.findIndex((obj) => obj.id == updatedTodo.id);
		todos[objIndex].todo = updatedTodo.todo;
		todos[objIndex].due = updatedTodo.due;
		saveTodos();

		showModal = false;
	};
</script>

<style>
	main {
		max-width: 700px;
		margin: 0 auto;
	}
</style>

<Modal {showModal} on:click={toggleModal}>
	<h3>Update Todo</h3>
	<EditForm todo={selectedTodo} on:updateTodo={handleUpdateTodo} />
</Modal>

<AddTodoForm on:addTodo={addTodo} />
<main>
	<TodoList {todos} on:deleteTodo={deleteTodo} on:editTodo={editTodo} />
</main>
