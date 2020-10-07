<script>
  import { createEventDispatcher } from "svelte";

  let errors = { todo: "", due: "" };
  let fields = { todo: "", due: "" };
  let valid = false;

  let dispatch = createEventDispatcher();

  const handleSubmit = () => {
    valid = true;

    if (fields.todo.trim().length < 5) {
      valid = false;
      errors.todo = "Todo must be at least 5 characters long";
    } else {
      errors.todo = "";
    }

    if (!fields.due) {
      valid = false;
      errors.due = "Invalid due date";
    } else {
      errors.due = "";
    }

    if (valid) {
      let todo = {
        id: Math.random(),
        todo: fields.todo,
        due: fields.due,
      };

      dispatch('addTodo', todo);

      fields = { todo: "", due: "" };
    }
  };
</script>

<style>
  form {
    width: 400px;
    margin: 0 auto;
    text-align: center;
  }
  .form-field {
    margin: 18px auto;
  }
  input {
    width: 100%;
    border-radius: 6px;
  }
  label {
    margin: 10px auto;
    text-align: left;
  }
  .error {
    color: red;
    margin-bottom: 5px;
  }
  button {
    border: 0;
    cursor: pointer;
    padding: 8px 20px;
    font-weight: bold;
    background: rgb(113, 202, 113);
    border-radius: 6px;
    color: white;
    box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.4);
    margin-top: 10px;
  }
</style>

<form on:submit|preventDefault={handleSubmit}>
  <div class="form-field">
    <label for="todo" />
    <input
      type="text"
      id="todo"
      bind:value={fields.todo}
      placeholder="Todo..." />
    <div class="error">{errors.todo}</div>
  <div class="form-field">
    <label for="due" />
    <input type="date" bind:value={fields.due} id="due" />
    <div class="error">{errors.due}</div>
  </div>
    <button>Add Todo</button>
  </div>
</form>
