<script lang="ts">
  import { writable } from 'svelte/store';
	import type { ITodo } from '$root/types/todo'

  import AddTodo from './AddTodo.svelte'
  import Todo from './Todo.svelte'
  import Filter from './Filter.svelte'

  // state
  let todos: ITodo[] = [
    { id: '1e4a59703af84', text: 'Todo 1', completed: true },
    { id: '9e09bcd7b9349', text: 'Todo 2', completed: false },
    { id: '9e4273a51a37c', text: 'Todo 3', completed: false },
    { id: '53ae48bf605cc', text: 'Todo 4', completed: false },
  ]

  // computed : total count
  $: todosAmount = todos.length

  // methods
  function generateRandomId(): string {
		return Math.random().toString(16).slice(2)
  }

  function addTodo(todo: string): void {
    let newTodo: ITodo = {
      id: generateRandomId(),
      text: todo,
      completed: false,
    }
    todos = [...todos, newTodo]  // append
    filteredTodos.set([...todos])
  }

  function toggleCompleted(event: MouseEvent): void {
    let { checked } = event.target as HTMLInputElement

    todos = todos.map((todo) => ({
      ...todo,
      completed: checked,
    }))  // update
  }

  function completeTodo(id: string): void {
    todos = todos.map((todo) => {
      if (todo.id === id) {
        todo.completed = !todo.completed
      }
      return todo
    })
    // 얕은 복사라서 연동 되는건가?
    filteredTodos.update((items) => items)
  }

  function removeTodo(id: string): void {
    todos = todos.filter((todo) => todo.id !== id)
    filteredTodos.update((todos)=>{
      return todos.filter((todo) => todo.id !== id)
    })
  }

  function removeCompleted(): number {
    todos = todos.filter((todo) => todo.completed === false)
    filteredTodos.set([...todos])
    return todos.length
  }

  // for Filter
  const filteredTodos = writable([...todos]);
  // let filteredTodos: ITodo[] = [...todos]
  const filterAll = () => {
    filteredTodos.set([...todos])
  }
  const filterActive = () => {
    filteredTodos.set(todos.filter((todo) => todo.completed === false))
  }
  const filterCompleted = () => {
    filteredTodos.set(todos.filter((todo) => todo.completed === true))
  }
</script>

<!-- {@debug todos} -->

<main>
  <h1 class="title">todos</h1>

  <section class="todos">
    <AddTodo {addTodo} {toggleCompleted} {todosAmount} />

    {#if todosAmount}
      <ul class="todo-list">
        {#each $filteredTodos as todo (todo.id)}
          <Todo {todo} {completeTodo} {removeTodo} />
        {/each}
      </ul>

      <Filter {todosAmount} {filterAll} {filterActive} {filterCompleted} {removeCompleted}/>
    {/if}
  </section>
</main>

<style>
  /* Todos */

  .title {
    font-size: var(--font-80);
    font-weight: inherit;
    text-align: center;
    color: var(--color-title);
  }

  .todos {
    --width: 500px;
    --todos-bg: hsl(0 0% 98%);
    --todos-text: hsl(220 20% 14%);

    width: var(--width);
    color: var(--todos-text);
    background-color: var(--todos-bg);
    border-radius: var(--radius-base);
    border: 1px solid var(--color-gray-90);
    box-shadow: 0 0 4px var(--shadow-1);
  }

  .todo-list {
    list-style: none;
  }
</style>