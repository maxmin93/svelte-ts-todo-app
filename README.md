# Svelte Todo App

참고 [Make A Svelte Todo App](https://joyofcode.xyz/svelte-todo-app)

![svelte-todo-app](/static/svelte-todo-app-crunch.png)

## Getting Started

Typescript 버전

```bash
$ npm create svelte@latest todo-app
$ cd todo-app
$ npm install
$ npm run dev
```

## Components

### Todos.svelte

- Todo 리스트를 보여주는 컴포넌트
  - todos : Todo 리스트의 상태를 관리
  - filteredTodos : Todo 리스트의 필터링 상태를 관리 (Writable Store)
- 하위 컴포넌트
  - Todo.svelte : Todo 리스트의 각 항목
  - AddTodo.svelte : Todo 리스트에 새로운 항목을 추가하는 컴포넌트
  - Filter.svelte : Todo 리스트의 필터링 컴포넌트

### Todo.svelte

- Todo 리스트의 각 항목
- 체크박스를 클릭하면 Todo 항목의 완료 여부를 토글
- 삭제 버튼을 클릭하면 Todo 항목을 삭제

### AddTodo.svelte

- Todo 리스트에 새로운 항목을 추가하는 컴포넌트
- Todo 항목의 내용을 입력하고 엔터를 누르면 Todo 리스트에 추가

### Filter.svelte

- Todo 리스트의 필터링 컴포넌트
- All, Active, Completed 버튼을 클릭하면 Todo 리스트의 필터링
- 'Clear Completed' 버튼을 클릭하면 완료된 Todo 항목을 삭제
- 현재 Todo 리스크 크기를 출력
