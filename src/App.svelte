<script>
  import Todo from "./Todo.svelte";

  let lastId = 0;
  let description = "";
  let todos = [createTodo("Uno"), createTodo("Dos")];

  $: uncompleted = todos.filter((t) => !t.completed).length;
  $: total = todos.length;
  $: completed = total - uncompleted;

  function addTodo() {
    todos = todos.concat(createTodo(description));
    description = "";
  }

  function createTodo(description) {
    return { id: ++lastId, description, completed: false };
  }

  function deleteCompleted() {
    todos = todos.filter((t) => !t.completed);
  }

  function deleteTodo(id) {
    todos = todos.filter((todo) => todo.id !== id);
  }

  function toggleCompleted(id) {
    todos = todos.map((t) =>
      t.id === id ? { ...t, completed: !t.completed } : t
    );
  }
</script>

<style>
  ul {
    list-style: none;
  }
</style>

<main>
  <h1>Todo List</h1>
  <p>
    {uncompleted} of {total} remaining
    <button on:click={deleteCompleted} disabled={completed < 1}>
      Delete completed
    </button>
  </p>
  <label for="todo">Todo:</label>
  <input id="todo" bind:value={description} />
  <button on:click={addTodo} disabled={description.length < 1}>Add todo</button>
  <ul>
    {#each todos as todo}
      <Todo
        {todo}
        on:delete={deleteTodo(todo.id)}
        on:toggleCompleted={toggleCompleted(todo.id)} />
    {/each}
  </ul>
</main>
