<script>
  import Todo from "./Todo.svelte";
  import Button from '@smui/button';
  import TextField from '@smui/textfield';
</script>

<main>
  <h1>My Svelte App with SMUI</h1>
  <TextField label="Enter text" />
  <Button>Click me</Button>
  <h3>To Do List</h3>
  <Todo />
</main>

<style>
  main {
    padding: 1rem;
  }
</style>