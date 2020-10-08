<script>
  import { createEventDispatcher } from "svelte";

  let dispatch = createEventDispatcher();
  export let todo;

  let errors = { todo: "", due: "" };
  let valid = false;

  const handleEdit = () => {
    valid = true;

    if (todo.todo.trim().length < 5) {
      valid = false;
      errors.todo = "Todo must be at least 5 characters long";
    } else {
      errors.todo = "";
    }

    if (!todo.due) {
      valid = false;
      errors.due = "Invalid due date";
    } else {
      errors.due = "";
    }

    if (valid) {      
      dispatch("updateTodo", todo);
    }
  };
</script>

<style>
  form {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  input {
    width: 300px;
    border-radius: 5px;
    margin: 10px 0;
  }
  button {
    border: none;
    border-radius: 5px;
    color: white;
    background: rgb(55, 161, 55);
    font-weight: bold;
    padding: 10px 25px;
    cursor: pointer;
    margin-top: 15px;
  }
  .error {
    color: red;
  }
</style>

<form on:submit|preventDefault={handleEdit}>
  <input type="text" bind:value={todo.todo} />
  <div class="error">{errors.todo}</div>
  <input type="date" bind:value={todo.due} />
  <div class="error">{errors.due}</div>
  <button>Update</button>
</form>
