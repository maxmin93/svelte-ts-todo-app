<script lang="ts">
  type FilterFuncType = () => void

  // param1: number
  export let todosAmount: number = 0
  // param2: function
  export let filterAll: FilterFuncType
  // param3: function
  export let filterActive: FilterFuncType
  // param4: function
  export let filterCompleted: FilterFuncType
  // param4: function
  export let removeCompleted: () => number
</script>

<div class="actions">
  <span class="todo-count">{todosAmount} left</span>
  <div class="filters">
    <button class="filter" on:click={filterAll}>All</button>
    <button class="filter" on:click={filterActive}>Active</button>
    <button class="filter" on:click={filterCompleted}>Completed</button>
  </div>
  <button class="clear-completed" on:click={()=>{
    removeCompleted()
  }}>Clear completed</button>
</div>

<style>
  /* Filters */

  .actions {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: var(--spacing-8) var(--spacing-16);
    font-size: 0.9rem;
    border-top: 1px solid var(--color-gray-90);
  }

  .actions:before {
    content: '';
    height: 40px;
    position: absolute;
    right: 0;
    bottom: 0;
    left: 0;
    box-shadow: 0 1px 1px hsla(0, 0%, 0%, 0.2), 0 8px 0 -3px hsl(0, 0%, 96%),
      0 9px 1px -3px hsla(0, 0%, 0%, 0.2), 0 16px 0 -6px hsl(0, 0%, 96%),
      0 17px 2px -6px hsla(0, 0%, 0%, 0.2);
    z-index: -1;
  }

  .filters {
    display: flex;
    gap: var(--spacing-4);
  }

  .filter {
    text-transform: capitalize;
    padding: var(--spacing-4) var(--spacing-8);
    border: 1px solid transparent;
    border-radius: var(--radius-base);
  }

  .filter:hover {
    border: 1px solid var(--color-highlight);
  }

  .selected {
    border-color: var(--color-highlight);
  }
</style>