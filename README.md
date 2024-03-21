<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Todo App</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="container">
    <h1>Todo App</h1>
    <input type="text" id="todoInput" placeholder="Add new todo">
    <button onclick="addTodo()">Add</button>
    <input type="text" id="searchInput" placeholder="Search todo">
    <ul id="todoList"></ul>
  </div>
  <script src="script.js"></script>
</body>
</html>

let todos = [];

function renderTodos() {
  const todoList = document.getElementById("todoList");
  todoList.innerHTML = "";
  todos.forEach((todo, index) => {
    const li = document.createElement("li");
    li.textContent = todo;
    const deleteButton = document.createElement("button");
    deleteButton.textContent = "Delete";
    deleteButton.addEventListener("click", () => deleteTodo(index));
    li.appendChild(deleteButton);
    todoList.appendChild(li);
  });
}

function addTodo() {
  const todoInput = document.getElementById("todoInput");
  const todo = todoInput.value.trim();
  if (todo !== "") {
    todos.push(todo);
    renderTodos();
    todoInput.value = "";
  }
}

function deleteTodo(index) {
  todos.splice(index, 1);
  renderTodos();
}

function searchTodo() {
  const searchInput = document.getElementById("searchInput").value.trim().toLowerCase();
  const filteredTodos = todos.filter(todo => todo.toLowerCase().includes(searchInput));
  renderFilteredTodos(filteredTodos);
}

function renderFilteredTodos(filteredTodos) {
  const todoList = document.getElementById("todoList");
  todoList.innerHTML = "";
  filteredTodos.forEach((todo, index) => {
    const li = document.createElement("li");
    li.textContent = todo;
    const deleteButton = document.createElement("button");
    deleteButton.textContent = "Delete";
    deleteButton.addEventListener("click", () => deleteTodo(todos.indexOf(todo)));
    li.appendChild(deleteButton);
    todoList.appendChild(li);
  });
}

document.getElementById("searchInput").addEventListener("input", searchTodo);

body {
  font-family: Arial, sans-serif;
}

.container {
  max-width: 400px;
  margin: 50px auto;
}

input[type="text"] {
  width: 70%;
  padding: 8px;
  margin-right: 10px;
}

button {
  padding: 8px 15px;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 5px;
}

