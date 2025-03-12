<script>
  import axios from "axios";
  import { onMount } from "svelte";
  import Card,  { Content,
                  PrimaryAction,
                  Actions,
                  ActionButtons,
                  ActionIcons }  from '@smui/card';
  import Button, { Label } from '@smui/button';

  let todos = [];
  let newTodo = "";

  // Fetch Todos from the Backend
  onMount(async () => {
    const response = await axios.get("http://localhost:3000/todos");
    todos = response.data;
  });

  // Add a New Todo
  async function addTodo() {
    if (newTodo.trim() === "") return;
    const response = await axios.post("http://localhost:3000/todos", { text: newTodo });
    todos = [...todos, response.data];
    newTodo = "";
  }

  // Delete a Todo
  async function deleteTodo(id) {
    await axios.delete(`http://localhost:3000/todos/${id}`);
    todos = todos.filter(todo => todo._id !== id);
  }

  async function removeTodo(id) {
    await deleteTodo(id);
    todos = todos.filter(todo => todo.id !== id);
  }
</script>

<style>

</style>

<h1>Todo List</h1>

<input type="text" bind:value={newTodo} placeholder="Add a new task" />
<button on:click={addTodo}>Add</button>

{#each todos as todo}
  <Card>
    <Card.Primary>
      <Card.Title>{todo.text}</Card.Title>
      <Card.Subtitle>{todo.completed ? 'Completed' : 'Pending'}</Card.Subtitle>
    </Card.Primary>
    <Card.Actions>
      <Button on:click={() => removeTodo(todo.id)}>Delete</Button>
    </Card.Actions>
  </Card>
{/each}

<!-- <ul>
  {#each todos as todo}
    <li class="todo">
      <span>{todo.text}</span>
      <button on:click={() => deleteTodo(todo._id)}>Delete</button>
    </li>
  {/each}
</ul> -->
