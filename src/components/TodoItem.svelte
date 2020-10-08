<script>
  import { createEventDispatcher } from "svelte";

  export let todo;

  let dispatch = createEventDispatcher();
</script>

<style>
  .todo {
    padding: 8px 20px;
    box-shadow: 1px 2px 4px rgba(0, 0, 0, 0.4);
    border-radius: 6px;
    margin: 15px 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  p {
    width: 100%;
    margin: 8px 0;
    text-align: left;
    font-size: 16px;
  }
  .due {
    font-size: 13px;
  }
  button {
    border: none;
    border-radius: 8px;
    font-weight: bold;
    color: white;
    background: crimson;
    padding: 5px 10px;
    cursor: pointer;
  }
</style>

<div class="todo">
  <div class="left">
    <p>{todo.todo}</p>
    <p class="due">{todo.due}</p>
  </div>

  <button
    on:click={() => {
      dispatch('deleteTodo', todo.id);
    }}>X</button>
</div>
