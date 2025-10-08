# MWAD-EX_03-To-Do-List-using-JavaScript
## Date: 7-10-25

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
### index.html
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Todo Application</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="todo-container">
    <h1>My To-Do List</h1>
    <div class="input-section">
      <input type="text" id="todo-input" placeholder="Add a new task...">
      <button id="add-btn">Add</button>
    </div>

    <ul id="todo-list"></ul>

    <div class="footer-section">
      <button id="clear-all">Clear All</button>
    </div>
  </div>

  <footer>
    <p>Created by <strong>Yaseen F</strong></p>
  </footer>

  <script src="script.js"></script>
</body>
</html>
```

### style.css
```
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}

body {
  background: linear-gradient(135deg, #3d9eff);
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.todo-container {
  background: red;
  width: 90%;
  max-width: 400px;
  padding: 25px;
  border-radius: 15px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
}

h1 {
  text-align: center;
  color: #2d3436;
  margin-bottom: 20px;
}

.input-section {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}

#todo-input {
  flex: 1;
  padding: 10px;
  border: 2px solid #0984e3;
  border-radius: 8px;
  outline: none;
}

#add-btn {
  background: #0984e3;
  color: white;
  border: none;
  padding: 10px 15px;
  border-radius: 8px;
  margin-left: 10px;
  cursor: pointer;
  transition: 0.3s;
}

#add-btn:hover {
  background: #74b9ff;
}

ul {
  list-style: none;
}

li {
  background: #dfe6e9;
  padding: 10px;
  border-radius: 8px;
  margin-bottom: 10px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

li.done {
  text-decoration: line-through;
  background: #b2bec3;
}

button.edit, button.delete {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 18px;
  margin-left: 8px;
}

button.delete {
  color: #d63031;
}

button.edit {
  color: #0984e3;
}

.footer-section {
  text-align: center;
  margin-top: 15px;
}

#clear-all {
  background: #d63031;
  color: white;
  padding: 8px 15px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: 0.3s;
}

#clear-all:hover {
  background: #ff7675;
}

footer {
  margin-top: 25px;
  text-align: center;
  color: white;
}
```

###  script.js
```
const input = document.getElementById("todo-input");
const addBtn = document.getElementById("add-btn");
const todoList = document.getElementById("todo-list");
const clearAllBtn = document.getElementById("clear-all");

document.addEventListener("DOMContentLoaded", loadTasks);

addBtn.addEventListener("click", addTask);
clearAllBtn.addEventListener("click", clearAll);

function addTask() {
  const taskText = input.value.trim();
  if (taskText === "") {
    alert("Please enter a task!");
    return;
  }

  const task = {
    text: taskText,
    completed: false
  };

  createTaskElement(task);
  saveTask(task);
  input.value = "";
}

function createTaskElement(task) {
  const li = document.createElement("li");
  li.textContent = task.text;
  if (task.completed) li.classList.add("done");

  li.addEventListener("click", () => {
    li.classList.toggle("done");
    updateStatus(task.text);
  });

  const btnGroup = document.createElement("div");

  const editBtn = document.createElement("button");
  editBtn.textContent = "✏️";
  editBtn.classList.add("edit");
  editBtn.addEventListener("click", (e) => {
    e.stopPropagation();
    const newText = prompt("Edit your task:", task.text);
    if (newText) {
      li.firstChild.textContent = newText;
      updateTask(task.text, newText);
    }
  });

  const delBtn = document.createElement("button");
  delBtn.textContent = "🗑️";
  delBtn.classList.add("delete");
  delBtn.addEventListener("click", (e) => {
    e.stopPropagation();
    li.remove();
    deleteTask(task.text);
  });

  btnGroup.appendChild(editBtn);
  btnGroup.appendChild(delBtn);
  li.appendChild(btnGroup);
  todoList.appendChild(li);
}

function saveTask(task) {
  const tasks = getTasks();
  tasks.push(task);
  localStorage.setItem("tasks", JSON.stringify(tasks));
}

function loadTasks() {
  const tasks = getTasks();
  tasks.forEach(createTaskElement);
}

function getTasks() {
  return JSON.parse(localStorage.getItem("tasks")) || [];
}

function deleteTask(taskText) {
  const tasks = getTasks().filter(t => t.text !== taskText);
  localStorage.setItem("tasks", JSON.stringify(tasks));
}

function updateTask(oldText, newText) {
  const tasks = getTasks();
  const index = tasks.findIndex(t => t.text === oldText);
  if (index !== -1) tasks[index].text = newText;
  localStorage.setItem("tasks", JSON.stringify(tasks));
}

function updateStatus(taskText) {
  const tasks = getTasks();
  const index = tasks.findIndex(t => t.text === taskText);
  if (index !== -1) tasks[index].completed = !tasks[index].completed;
  localStorage.setItem("tasks", JSON.stringify(tasks));
}

function clearAll() {
  localStorage.removeItem("tasks");
  todoList.innerHTML = "";
}
```


## OUTPUT
<img width="1384" height="680" alt="Screenshot 2025-10-08 105158" src="https://github.com/user-attachments/assets/ebcc65c7-954c-46db-acee-ea2d7e2874f6" />



## RESULT
The program for creating To-do list using JavaScript is executed successfully.
