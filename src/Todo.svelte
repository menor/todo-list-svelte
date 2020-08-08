<script>
  import { createEventDispatcher } from "svelte";
  import App from "./App.svelte";

  const dispatch = createEventDispatcher();

  export let todo;
</script>

<style>
  .completed {
    text-decoration: line-through;
  }
</style>

<li class={todo.completed && 'completed'}>
  <input
    id="complete"
    type="checkbox"
    checked={todo.completed}
    on:change={() => dispatch('toggleCompleted')} />
  {todo.description}
  <button on:click={() => dispatch('delete')}>Delete</button>
</li>
