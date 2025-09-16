# MWAD-EX_03-To-Do-List-using-JavaScript
## Date: 16/09/2025

## AIM
To create a To-do Application with all features using JavaScript.

## ALGORITHM
### STEP 1
Build the HTML structure (index.html).

### STEP 2
Style the App (style.css).

### STEP 3
Plan the features the To-Do App should have.

### STEP 4
Create a To-do application using Javascript.

### STEP 5
Add functionalities.

### STEP 6
Test the App.

### STEP 7
Open the HTML file in a browser to check layout and functionality.

### STEP 8
Fix styling issues and refine content placement.

### STEP 9
Deploy the website.

### STEP 10
Upload to GitHub Pages for free hosting.

## PROGRAM
index.html
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>To-Do App</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="todo-container">
    <h1>To-Do List</h1>
    <div class="input-section">
      <input type="text" id="taskInput" placeholder="Add a new task...">
      <button id="addBtn">Add</button>
    </div>
    <ul id="taskList"></ul>
  </div>

  <!-- JavaScript will be linked later -->
  <script src="script.js"></script>
</body>
</html>
```

style.css
```
/* General Page Styling */
body {
  font-family: Arial, sans-serif;
  background: #f4f6f8;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  height: 100vh;
  margin: 0;
  padding-top: 50px;
}

/* To-do Container */
.todo-container {
  background: #fff;
  padding: 20px 25px;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0,0,0,0.1);
  width: 350px;
}

h1 {
  text-align: center;
  color: #333;
  margin-bottom: 20px;
}

/* Input Section */
.input-section {
  display: flex;
  margin-bottom: 15px;
}

.input-section input {
  flex: 1;
  padding: 10px;
  border: 2px solid #ddd;
  border-radius: 5px 0 0 5px;
  outline: none;
}

.input-section button {
  padding: 10px 15px;
  background: #4caf50;
  border: none;
  color: white;
  font-weight: bold;
  cursor: pointer;
  border-radius: 0 5px 5px 0;
  transition: background 0.3s;
}

.input-section button:hover {
  background: #45a049;
}

/* Task List */
#taskList {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

#taskList li {
  background: #f9f9f9;
  margin-bottom: 10px;
  padding: 10px;
  border-radius: 5px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

#taskList li.completed {
  text-decoration: line-through;
  color: gray;
}

.task-buttons {
  display: flex;
  gap: 8px;
}

.task-buttons button {
  border: none;
  padding: 5px 8px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 12px;
}

.task-buttons .delete {
  background: #e74c3c;
  color: white;
}

.task-buttons .edit {
  background: #3498db;
  color: white;
}
```
script.js
```
// Select elements
const taskInput = document.getElementById("taskInput");
const addBtn = document.getElementById("addBtn");
const taskList = document.getElementById("taskList");

// Load tasks from localStorage
document.addEventListener("DOMContentLoaded", loadTasks);

// Add Task
addBtn.addEventListener("click", addTask);
taskInput.addEventListener("keypress", (e) => {
  if (e.key === "Enter") addTask();
});

function addTask() {
  const taskText = taskInput.value.trim();
  if (taskText === "") {
    alert("Please enter a task!");
    return;
  }

  createTaskElement(taskText);
  saveTask(taskText);
  taskInput.value = "";
}

// Create Task Element
function createTaskElement(taskText, completed = false) {
  const li = document.createElement("li");
  if (completed) li.classList.add("completed");

  const span = document.createElement("span");
  span.textContent = taskText;
  span.addEventListener("click", () => toggleComplete(li, taskText));

  // Buttons (Edit + Delete)
  const btnContainer = document.createElement("div");
  btnContainer.classList.add("task-buttons");

  const editBtn = document.createElement("button");
  editBtn.textContent = "Edit";
  editBtn.classList.add("edit");
  editBtn.addEventListener("click", () => editTask(span, taskText));

  const deleteBtn = document.createElement("button");
  deleteBtn.textContent = "Delete";
  deleteBtn.classList.add("delete");
  deleteBtn.addEventListener("click", () => deleteTask(li, taskText));

  btnContainer.appendChild(editBtn);
  btnContainer.appendChild(deleteBtn);

  li.appendChild(span);
  li.appendChild(btnContainer);

  taskList.appendChild(li);
}

// Toggle Task Completion
function toggleComplete(li, taskText) {
  li.classList.toggle("completed");
  updateTaskStatus(taskText, li.classList.contains("completed"));
}

// Edit Task
function editTask(span, oldText) {
  const newText = prompt("Edit your task:", span.textContent);
  if (newText && newText.trim() !== "") {
    span.textContent = newText.trim();
    updateTaskText(oldText, newText.trim());
  }
}

// Delete Task
function deleteTask(li, taskText) {
  if (confirm("Are you sure you want to delete this task?")) {
    li.remove();
    removeTask(taskText);
  }
}

/* --------------------------
   LocalStorage Functions
-------------------------- */
function saveTask(taskText) {
  let tasks = getTasks();
  tasks.push({ text: taskText, completed: false });
  localStorage.setItem("tasks", JSON.stringify(tasks));
}

function getTasks() {
  return JSON.parse(localStorage.getItem("tasks")) || [];
}

function loadTasks() {
  const tasks = getTasks();
  tasks.forEach((task) => {
    createTaskElement(task.text, task.completed);
  });
}

function updateTaskStatus(taskText, completed) {
  let tasks = getTasks();
  tasks = tasks.map((task) =>
    task.text === taskText ? { ...task, completed } : task
  );
  localStorage.setItem("tasks", JSON.stringify(tasks));
}

function updateTaskText(oldText, newText) {
  let tasks = getTasks();
  tasks = tasks.map((task) =>
    task.text === oldText ? { ...task, text: newText } : task
  );
  localStorage.setItem("tasks", JSON.stringify(tasks));
}

function removeTask(taskText) {
  let tasks = getTasks();
  tasks = tasks.filter((task) => task.text !== taskText);
  localStorage.setItem("tasks", JSON.stringify(tasks));
}
```

## OUTPUT

<img width="608" height="358" alt="Screenshot 2025-09-16 102753" src="https://github.com/user-attachments/assets/27a699ef-ff72-4273-b538-d15e5469e9ca" />

<img width="1700" height="643" alt="Screenshot 2025-09-16 103056" src="https://github.com/user-attachments/assets/2c6bda99-cb54-41e8-8f1e-d2e3e1dc8bce" />

## RESULT
The program for creating To-do list using JavaScript is executed successfully.
