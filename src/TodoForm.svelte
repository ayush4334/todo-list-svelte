<script>
  import Title from "./Title.svelte";
  export let name = "";
  // export let amount = null;
  export let addTodo;
  export let isEditing;
  export let editTodo;
  export let hideForm;
  $: isEmpty = !name;

  function handleSubmit() {
    if (isEditing) editTodo({ name });
    else addTodo({ name });
    name = "";
    // amount = null;
    hideForm();
  }
</script>

<section class="form">
  <Title title="Add To-do" />
  <form class="expense-form" on:submit|preventDefault={handleSubmit}>
    <div class="form-control">
      <label for="name">name</label>
      <input type="text" id="name" bind:value={name} />
    </div>
    {#if isEmpty}
      <p class="form-empty">please fill out all form fields!</p>
    {/if}
    <button
      type="submit"
      class="btn btn-block"
      class:disabled={isEmpty}
      disabled={isEmpty}>
      {#if isEditing}Edit To-do{:else}Add To-do{/if}
    </button>
    <button type="button" class="close-btn" on:click={hideForm}>
      <i class="fas fa-times" />
      close
    </button>
  </form>
</section>
