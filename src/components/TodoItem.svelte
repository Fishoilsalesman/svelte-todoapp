<script>
  export let todo;
</script>

<style>
  .todo {    
    padding: 8px 20px;
    box-shadow: 1px 2px 4px rgba(0, 0, 0, 0.4);
    border-radius: 6px;    
    margin: 15px 0;
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
</style>

<div class="todo">
  <p>{todo.todo}</p>
  <p class="due">{todo.due}</p>
</div>