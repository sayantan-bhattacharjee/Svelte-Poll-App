<script>
  export let items
  export let activeItems

  import { createEventDispatcher } from "svelte"
  const dispatch = createEventDispatcher()
</script>

<div class="Tabs">
  <ul>
    {#each items as item, index}
      <li key={index} on:click={() => dispatch("tabchange", item)}>
        <div class:active={item === activeItems}>{item}</div>
      </li>
    {/each}
  </ul>
</div>

<style>
  .Tabs {
    margin-bottom: 40px;
  }
  ul {
    display: flex;
    justify-content: center;
    padding: 0px;
    list-style-type: none;
  }
  li {
    margin: 0px 16px;
    font-size: 18px;
    color: #555;
    cursor: pointer;
  }
  .active {
    color: #d91b42;
    border-bottom: 2px solid #d91b42;
    padding-bottom: 8px;
  }
</style>
