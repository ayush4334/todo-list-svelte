<script>
  import { getContext } from "svelte";
  export let id;
  export let name;
  
  const removeTodo = getContext("remove");
  const setModifiedTodo = getContext("modify");
</script>

<article class="single-expense">
  <div class="expense-info">
    <h2>
      {name}
    </h2>
  </div>
  <div class="expense-buttons">
    <button
      class="expense-btn edit-btn"
      on:click={() => setModifiedTodo(id)}>
      <i class="fas fa-pen" />
    </button>
    <button class="expense-btn delete-btn" on:click={() => removeTodo(id)}>
      <i class="fas fa-trash" />
    </button>
  </div>
</article>
