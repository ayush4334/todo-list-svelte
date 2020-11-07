<script>
  import SectionTitle from "./Title.svelte";
  import Todo from "./Todo.svelte";
  import { fly } from "svelte/transition";
  import { flip } from "svelte/animate";
  export let todos = [];
</script>

<style>
  h2 {
    text-transform: capitalize;
  }
</style>

<section>
  <SectionTitle title="To-do List" />
  <ul>
    {#each todos as todo, index (todo.id)}
      <div
        in:fly={{ x: 200, delay: (index + 1) * 500 }}
        out:fly={{ x: -200 }}
        animate:flip>
        <Todo {...todo} />
      </div>
    {:else}
      <h2>No To-dos added to the list!!</h2>
    {/each}
  </ul>
</section>
