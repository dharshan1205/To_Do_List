# MWAD-EX_03-To-Do-List-using-JavaScript
## Date: 10/03/2025

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
## Index.html
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Colorful To-Do List</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="todo-container">
    <h1>🌈 My To-Do List</h1>

    <div class="input-section">
      <input type="text" id="task-input" placeholder="Add a new task...">
      <input type="date" id="task-date">
      <select id="task-priority">
        <option value="low">🟢 Low</option>
        <option value="medium">🟡 Medium</option>
        <option value="high">🔴 High</option>
      </select>
      <button id="add-btn">Add Task</button>
    </div>

    <ul id="task-list"></ul>
    <button id="clear-btn">Clear All</button>
  </div>

  <script src="script.js"></script>
</body>
</html>

```
## Style.css
```
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

body {
  background: linear-gradient(to right, #fbc2eb, #a6c1ee);
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.todo-container {
  background: #fff;
  padding: 30px;
  border-radius: 15px;
  width: 450px;
  box-shadow: 0 8px 25px rgba(0,0,0,0.3);
  text-align: center;
}

.todo-container h1 {
  color: #333;
  margin-bottom: 20px;
}

.input-section {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  gap: 10px;
  margin-bottom: 20px;
}

#task-input {
  flex: 2;
  padding: 10px;
  border: 2px solid #ddd;
  border-radius: 5px;
  font-size: 16px;
}

#task-date, #task-priority {
  flex: 1;
  padding: 10px;
  border-radius: 5px;
  border: 2px solid #ddd;
  font-size: 14px;
}

#add-btn {
  padding: 10px 15px;
  border: none;
  background-color: #6a0dad;
  color: white;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.3s;
}

#add-btn:hover {
  background-color: #8e2de2;
}

#task-list {
  list-style: none;
  max-height: 300px;
  overflow-y: auto;
  padding: 0;
}

#task-list li {
  padding: 12px;
  margin-bottom: 10px;
  border-radius: 8px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  transition: 0.2s;
  background: #f0f0f0;
}

#task-list li.completed span {
  text-decoration: line-through;
  color: #888;
}

.task-btns button {
  background: none;
  border: none;
  margin-left: 8px;
  cursor: pointer;
  font-size: 16px;
}

.task-btns button.edit { color: #2196F3; }
.task-btns button.delete { color: #f44336; }

#clear-btn {
  margin-top: 15px;
  padding: 12px;
  width: 100%;
  border: none;
  background: #ff5722;
  color: white;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.3s;
}

#clear-btn:hover {
  background: #e64a19;
}

/* Priority Colors */
.low { border-left: 5px solid #4caf50; }
.medium { border-left: 5px solid #ffc107; }
.high { border-left: 5px solid #f44336; }
```
## Script.js
```
const input = document.getElementById("task-input");
const dateInput = document.getElementById("task-date");
const priorityInput = document.getElementById("task-priority");
const addBtn = document.getElementById("add-btn");
const taskList = document.getElementById("task-list");
const clearBtn = document.getElementById("clear-btn");

// Load tasks from localStorage
let tasks = JSON.parse(localStorage.getItem("tasks")) || [];
renderTasks();

// Add Task
addBtn.addEventListener("click", () => {
    const taskText = input.value.trim();
    const taskDate = dateInput.value;
    const taskPriority = priorityInput.value;

    if(taskText) {
        const task = {
            text: taskText,
            date: taskDate,
            priority: taskPriority,
            completed: false
        };
        tasks.push(task);
        saveTasks();
        renderTasks();
        input.value = "";
        dateInput.value = "";
        priorityInput.value = "low";
    }
});

// Render Tasks
function renderTasks() {
    taskList.innerHTML = "";
    tasks.forEach((task, index) => {
        const li = document.createElement("li");
        li.className = task.priority + (task.completed ? " completed" : "");
        li.innerHTML = `
            <span>${task.text} ${task.date ? "| 📅 " + task.date : ""}</span>
            <div class="task-btns">
                <button class="edit">✏️</button>
                <button class="delete">🗑️</button>
            </div>
        `;
        taskList.appendChild(li);

        // Toggle complete
        li.querySelector("span").addEventListener("click", () => {
            tasks[index].completed = !tasks[index].completed;
            saveTasks();
            renderTasks();
        });

        // Edit
        li.querySelector(".edit").addEventListener("click", () => {
            const newText = prompt("Edit task:", tasks[index].text);
            if(newText) {
                tasks[index].text = newText;
                saveTasks();
                renderTasks();
            }
        });

        // Delete
        li.querySelector(".delete").addEventListener("click", () => {
            tasks.splice(index, 1);
            saveTasks();
            renderTasks();
        });
    });
}

// Clear all tasks
clearBtn.addEventListener("click", () => {
    if(confirm("Are you sure you want to clear all tasks?")) {
        tasks = [];
        saveTasks();
        renderTasks();
    }
});

// Save tasks to localStorage
function saveTasks() {
    localStorage.setItem("tasks", JSON.stringify(tasks));
}
```

## OUTPUT
## LOW PRIORITY
<img width="1905" height="974" alt="image" src="https://github.com/user-attachments/assets/9340c245-1805-4a4d-a51b-7bb8d83c1609" />

## MEDIUM PRIORITY
<img width="1902" height="976" alt="image" src="https://github.com/user-attachments/assets/fbace6b2-0da1-4706-8f07-53e7468371e0" />

## HIGH PRIORITY
<img width="1910" height="928" alt="image" src="https://github.com/user-attachments/assets/f5412957-d89d-4800-a0e8-f4c2d6fa9e88" />




## RESULT
The program for creating To-do list using JavaScript is executed successfully.
