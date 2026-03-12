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
    <title>Advanced Todo App</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <div class="todo-container">
        <h2>My Task Manager</h2>
        
        <div class="input-group">
            <input type="text" id="taskInput" placeholder="What needs to be done?">
            <input type="datetime-local" id="reminderInput">
            <button onclick="addTask()">Add Task</button>
        </div>

        <ul id="taskList"></ul>

        <div class="footer">
            <p><strong>Name:</strong> DHARSHAN R</p>
            <p><strong>Reg No:</strong> 212224230060</p>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>
```
## Style.css
```
body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background-color: #f4f7f6;
    display: flex;
    justify-content: center;
    padding: 50px;
}

.todo-container {
    background: white;
    padding: 2rem;
    border-radius: 12px;
    box-shadow: 0 10px 25px rgba(0,0,0,0.1);
    width: 100%;
    max-width: 450px;
}

h2 { text-align: center; color: #333; }

.input-group {
    display: flex;
    flex-direction: column;
    gap: 10px;
    margin-bottom: 20px;
}

input {
    padding: 12px;
    border: 1px solid #ddd;
    border-radius: 6px;
}

button {
    padding: 12px;
    background-color: #28a745;
    color: white;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-weight: bold;
}

button:hover { background-color: #218838; }

ul { list-style: none; padding: 0; }

li {
    background: #fff;
    border-bottom: 1px solid #eee;
    padding: 10px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.task-info { display: flex; flex-direction: column; }
.reminder-text { font-size: 0.8rem; color: #888; }

.delete-btn {
    background: #dc3545;
    padding: 5px 10px;
    font-size: 0.8rem;
}

.footer {
    margin-top: 30px;
    padding-top: 15px;
    border-top: 2px solid #eee;
    text-align: center;
    font-size: 0.9rem;
    color: #555;
}
```
## Script.js
```
// Request permission for notifications on load
if (Notification.permission !== "granted") {
    Notification.requestPermission();
}

function addTask() {
    const taskInput = document.getElementById('taskInput');
    const reminderInput = document.getElementById('reminderInput');
    const taskList = document.getElementById('taskList');

    if (taskInput.value === '') {
        alert("Please enter a task!");
        return;
    }

    const li = document.createElement('li');
    const taskTime = reminderInput.value ? new Date(reminderInput.value).toLocaleString() : "No reminder";

    li.innerHTML = `
        <div class="task-info">
            <strong>${taskInput.value}</strong>
            <span class="reminder-text">🔔 ${taskTime}</span>
        </div>
        <button class="delete-btn" onclick="this.parentElement.remove()">Delete</button>
    `;

    // Logic for the reminder
    if (reminderInput.value) {
        const triggerTime = new Date(reminderInput.value).getTime();
        const currentTime = new Date().getTime();
        const delay = triggerTime - currentTime;

        if (delay > 0) {
            setTimeout(() => {
                new Notification("Task Reminder!", {
                    body: `Time to: ${taskInput.value}`,
                    icon: "https://cdn-icons-png.flaticon.com/512/1792/1792931.png"
                });
                li.style.backgroundColor = "#fff3cd"; // Highlight task when reminder hits
            }, delay);
        }
    }

    taskList.appendChild(li);
    
    // Clear inputs
    taskInput.value = '';
    reminderInput.value = '';
}
```

## OUTPUT
<img width="1917" height="1148" alt="image" src="https://github.com/user-attachments/assets/0cb3d55c-0c09-4660-9665-49adba3a9334" />

<img width="1920" height="1144" alt="image" src="https://github.com/user-attachments/assets/0c6de924-fcaa-46eb-9ed4-1611471f2816" />


## RESULT
The program for creating To-do list using JavaScript is executed successfully.
