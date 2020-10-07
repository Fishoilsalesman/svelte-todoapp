<script>
  import TodoItem from "./TodoItem.svelte";

  export let todos;
</script>

<style>  
</style>

<div>
  {#each todos as todo (todo.id)}
    <TodoItem {todo} />
  {/each}
</div>
