<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Homework Tracker</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f8ff;
            margin: 0;
            padding: 20px;
            color: #333;
        }
        h1 {
            text-align: center;
            color: #0066cc;
        }
        .task-container {
            max-width: 600px;
            margin: auto;
            padding: 20px;
            background: white;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        .task {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 0;
            border-bottom: 1px solid #ddd;
        }
        .task:last-child {
            border-bottom: none;
        }
        .add-task {
            display: flex;
            justify-content: space-between;
            margin-top: 20px;
            gap: 10px;
        }
        input[type="text"], input[type="date"], select {
            flex: 1;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            padding: 10px;
            border: none;
            background-color: #0066cc;
            color: white;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #005bb5;
        }
        .ca-link {
            display: block;
            text-align: center;
            margin: 20px auto;
            background-color: #ff6600;
            color: white;
            padding: 10px 15px;
            border-radius: 5px;
            text-decoration: none;
            font-weight: bold;
            width: fit-content;
        }
        .search-bar {
            margin-bottom: 20px;
            display: flex;
            justify-content: space-between;
            gap: 10px;
        }
        @media (max-width: 600px) {
            .add-task, .search-bar {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <h1>Homework Tracker</h1>
    <a href="http://10.240.1.89/academic_history" class="ca-link" target="_blank">
        Check Continuous Assessment
    </a>
    <div class="task-container">
        <div class="search-bar">
            <input type="text" id="searchTask" placeholder="Search tasks..." onkeyup="searchTasks()">
        </div>
        <div id="tasks"></div>
        <div class="add-task">
            <input type="text" id="taskName" placeholder="Task name">
            <input type="date" id="taskDate">
            <select id="taskPriority">
                <option value="Low">Low Priority</option>
                <option value="Medium">Medium Priority</option>
                <option value="High">High Priority</option>
            </select>
            <button onclick="addTask()">Add Task</button>
        </div>
    </div>
    <script>
        function addTask() {
            const taskName = document.getElementById('taskName').value;
            const taskDate = document.getElementById('taskDate').value;
            const taskPriority = document.getElementById('taskPriority').value;

            if (taskName && taskDate) {
                const tasksDiv = document.getElementById('tasks');
                const taskDiv = document.createElement('div');
                taskDiv.className = 'task';
                taskDiv.innerHTML = `
                    <span>${taskName} - ${taskDate} [${taskPriority}]</span>
                    <button onclick="removeTask(this)">Remove</button>
                `;
                tasksDiv.appendChild(taskDiv);
                document.getElementById('taskName').value = '';
                document.getElementById('taskDate').value = '';
            } else {
                alert('Please fill out both fields!');
            }
        }

        function removeTask(button) {
            button.parentElement.remove();
        }

        function searchTasks() {
            const searchValue = document.getElementById('searchTask').value.toLowerCase();
            const tasks = document.getElementById('tasks').children;

            for (const task of tasks) {
                const text = task.textContent.toLowerCase();
                task.style.display = text.includes(searchValue) ? '' : 'none';
            }
        }
    </script>
</body>
</html>