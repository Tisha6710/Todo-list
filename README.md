# Todo-list
I have a created a simple project of Todo list using HTML,CSS AND JAVASCRIPT.
<!DOCTYPE html>
<html lang="en">
<head>
  <title>TaskMaster - To-Do List</title>
  <style>
    /* General Styles */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: "Poppins", sans-serif;
    }

    body {
      background: linear-gradient(135deg, #1c1c1c, #34495e);
      display: flex;
      flex-direction: column;
      align-items: center;
      min-height: 100vh;
      color: white;
    }

    /* Navbar */
    .navbar {
      width: 100%;
      background: rgba(0, 0, 0, 0.9);
      color: white;
      padding: 18px;
      text-align: center;
      font-size: 24px;
      font-weight: bold;
      letter-spacing: 1px;
    }

    /* Main Container */
    .container {
      background: #222;
      padding: 30px;
      border-radius: 12px;
      box-shadow: 0px 8px 20px rgba(255, 255, 255, 0.1);
      width: 500px;
      text-align: center;
      margin-top: 40px;
      transition: 0.3s;
    }

    .container:hover {
      transform: scale(1.02);
    }

    h1 {
      color: #f1c40f;
      margin-bottom: 15px;
    }

    /* Input & Button Layout */
    .grid-container {
      display: grid;
      grid-template-columns: 1fr 1fr auto;
      gap: 12px;
      margin-bottom: 20px;
    }

    input {
      font-size: 15px;
      padding: 12px;
      border: 1px solid #555;
      border-radius: 8px;
      width: 100%;
      background: #333;
      color: white;
    }

    input:focus {
      outline: none;
      border-color: #f1c40f;
      box-shadow: 0px 0px 8px rgba(241, 196, 15, 0.5);
    }

    /* Buttons */
    .btn {
      padding: 12px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-size: 15px;
      transition: 0.3s;
    }

    .btn-add {
      background-color: #f1c40f;
      color: black;
      font-weight: bold;
    }

    .btn-add:hover {
      background-color: #d4ac0d;
    }

    .btn-delete {
      background-color: #e74c3c;
      color: white;
      font-weight: bold;
    }

    .btn-delete:hover {
      background-color: #c0392b;
    }

    .btn-clear {
      background-color: #3498db;
      color: white;
      margin-top: 10px;
      width: 100%;
      font-weight: bold;
    }

    .btn-clear:hover {
      background-color: #2980b9;
    }

    /* Task List */
    .todo-container {
      max-height: 300px;
      overflow-y: auto;
      margin-top: 15px;
      padding-right: 10px;
    }

    .todo-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      background: #333;
      padding: 12px;
      border-radius: 8px;
      box-shadow: 0px 2px 5px rgba(255, 255, 255, 0.1);
      margin-bottom: 10px;
      transition: 0.3s ease-in-out;
      color: white;
    }

    .todo-item:hover {
      transform: scale(1.03);
      background: #444;
    }

    /* Scrollbar Styling */
    .todo-container::-webkit-scrollbar {
      width: 6px;
    }

    .todo-container::-webkit-scrollbar-thumb {
      background: #f1c40f;
      border-radius: 10px;
    }

    /* Footer */
    .footer {
        position: fixed;
  bottom: 0;
  width: 100%;
  text-align: center;
  font-size: 14px;
  padding: 12px;
  background: rgba(0, 0, 0, 0.9);
  color: white;
  letter-spacing: 1px;
    }

  </style>
</head>
<body>

  <!-- Navbar -->
  <div class="navbar">📝 TaskMaster - Your To-Do Manager</div>

  <!-- Main Box -->
  <div class="container">
    <h1>Manage Your Tasks Efficiently</h1>

    <div class="grid-container">
      <input id="todo-input" type="text" placeholder="Enter a task">
      <input id="todo-date" type="date">
      <button class="btn btn-add" onclick="addTodo()">➕ Add</button>
    </div>

    <div class="todo-container"></div>

    <button class="btn btn-clear" onclick="clearAll()">🗑 Clear All</button>
  </div>

  <!-- Footer -->
  <div class="footer">© 2025 All Rights Reserved | TaskMaster</div>

  <script>
    let todoList = JSON.parse(localStorage.getItem('todos')) || [];

    displayItems();

    function addTodo() {
      let inputElement = document.querySelector('#todo-input');
      let dateElement = document.querySelector('#todo-date');
      let todoItem = inputElement.value.trim();
      let todoDate = dateElement.value;

      if (todoItem === '' || todoDate === '') {
        alert('Please enter both task and date!');
        return;
      }

      todoList.push({ item: todoItem, dueDate: todoDate });
      localStorage.setItem('todos', JSON.stringify(todoList));

      inputElement.value = '';
      dateElement.value = '';
      displayItems();
    }

    function displayItems() {
      let containerElement = document.querySelector('.todo-container');
      containerElement.innerHTML = '';

      todoList.forEach((todo, index) => {
        let todoItemDiv = document.createElement('div');
        todoItemDiv.classList.add('todo-item');
        todoItemDiv.innerHTML = `
          <span>📌 ${todo.item}</span>
          <span>📅 ${todo.dueDate}</span>
          <button class='btn btn-delete' onclick="deleteTodo(${index})">❌</button>
        `;
        containerElement.appendChild(todoItemDiv);
      });
    }

    function deleteTodo(index) {
      todoList.splice(index, 1);
      localStorage.setItem('todos', JSON.stringify(todoList));
      displayItems();
    }

    function clearAll() {
      if (confirm("Are you sure you want to delete all tasks?")) {
        todoList = [];
        localStorage.removeItem('todos');
        displayItems();
      }
    }
  </script>
</body>
</html>

