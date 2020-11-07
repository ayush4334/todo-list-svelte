<script>
  import { setContext, onMount } from "svelte";
  import Navbar from "./Navbar.svelte";
  import TodosList from "./TodosList.svelte";
  import TodoForm from "./TodoForm.svelte";
  import Modals from "./Modal.svelte";

  let todos = [];

  let setId = null;
  let setName = "";
  let isFormOpen = false;
  $: isEditing = setId ? true : false;
  
  function removeTodo(id) {
    todos = todos.filter(item => item.id != id);
    setLocalStorage();
  }

  setContext("remove", removeTodo);
  setContext("modify", setModifiedTodo);

  function clearTodos() {
    todos = [];
    setLocalStorage();
  }

  function addTodo({ name }) {
    let todo = { id: Math.random() * Date.now(), name };
    todos = [todo, ...todos];
    setLocalStorage();
  }

  function setModifiedTodo(id) {
    let todo = todos.find(item => item.id === id);
    setId = todo.id;
    setName = todo.name;
    showForm();
  }

  function editTodo({ name }) {
    todos = todos.map(item => {
      return item.id === setId ? { ...item, name } : { ...item };
    });
    setId = null;
    setName = "";
    setLocalStorage();
  }

  function showForm() {
    isFormOpen = true;
  }

  function hideForm() {
    isFormOpen = false;
    setId = null;
    setName = "";
    setAmount = null;
  }

  function setLocalStorage() {
    localStorage.setItem("todos", JSON.stringify(todos));
  }

  onMount(() => {
    todos = localStorage.getItem("todos")
      ? JSON.parse(localStorage.getItem("todos"))
      : [];
  });
</script>

<Navbar {showForm} />
<main class="content">
  {#if isFormOpen}
    <Modals>
		<TodoForm
        {addTodo}
        name={setName}
        {isEditing}
        {editTodo}
        {hideForm} />
    </Modals>
  {/if}
  <TodosList {todos} />
  <button
    type="button"
    class="btn btn-primary btn-block"
    on:click={clearTodos}>
    Clear Todos
  </button>
</main>
