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

      dispatch("addTodo", todo);

      fields = { todo: "", due: "" };
    }
  };
</script>

<style>
  form {
    display: flex;
    flex-direction: row;
    justify-content: center;    
    padding-top: 40px;
  }
  .form-field {
    margin: 5px 10px;
  }
  input#todo {
    width: 400px;
  }
  input#due {
    width: 150px;
  }
  input {
    border-radius: 6px;
  }
  .error {
    color: red;
    margin-bottom: 5px;
    margin-left: 5px;
  }
  button {
    border: 0;
    cursor: pointer;
    padding: 8px 20px;
    font-weight: bold;
    background: rgb(113, 202, 113);
    border-radius: 6px;
    color: white;
  }
</style>

<form on:submit|preventDefault={handleSubmit}>
  <div class="form-field">
    <input
      type="text"
      id="todo"
      bind:value={fields.todo}
      placeholder="Todo..." />
    <div class="error">{errors.todo}</div>
  </div>
  <div class="form-field">
    <input type="date" bind:value={fields.due} id="due" />
    <div class="error">{errors.due}</div>
  </div>
  <div class="form-field"><button>Add Todo</button></div>
</form>
