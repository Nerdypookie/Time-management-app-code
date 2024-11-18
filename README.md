<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Time Management App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #131313;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            background-color: #e74c3c;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            width: 80%;
            max-width: 500px;
        }
        h1 {
            text-align: center;
            margin-bottom: 20px;
        }
        p {
             text-align: center;
             margin-bottom:20px;
             font-size:20px;
        }
        .form-group {
            margin-bottom: 15px;
        }
        input, button {
            width: 100%;
            padding: 10px;
            margin: 5px 0;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 16px;
        }
        button {
            background-color: #4CAF50;
            color: white;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        .task-list {
            margin-top: 20px;
            list-style: none;
            padding: 0;
        }
        .task-item {
            padding: 10px;
            border-bottom: 1px solid #ddd;
        }
        .task-item:last-child {
            border-bottom: none;
        }
        .task-info {
            font-size: 14px;
            color: #555;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Time It! </h1>
        <p> The future is better if you plan it</p>
       
        <div class="form-group">
            <input type="text" id="task-name" placeholder="Enter task name" />
        </div>
        <div class="form-group">
            <input type="number" id="task-duration" placeholder="Enter duration (minutes)" min="1" />
        </div>
        <button id="start-task">Start Task</button>

        
        <ul class="task-list" id="task-list"></ul>
    </div>

    <script>
        
        let taskList = [];
        const taskNameInput = document.getElementById('task-name');
        const taskDurationInput = document.getElementById('task-duration');
        const taskListContainer = document.getElementById('task-list');
        const startTaskButton = document.getElementById('start-task');

        function startTask() {
            const taskName = taskNameInput.value.trim();
            const taskDuration = parseInt(taskDurationInput.value);

            if (taskName && taskDuration > 0) {
               
                const startTime = new Date();
                const endTime = new Date(startTime.getTime() + taskDuration * 60000); 

                const task = {
                    name: taskName,
                    startTime: startTime,
                    endTime: endTime,
                    duration: taskDuration
                };

                taskList.push(task);

                renderTaskList();
                taskNameInput.value = '';
                taskDurationInput.value = '';
            } else {
                alert("Please enter valid task name and duration.");
            }
        }

        function renderTaskList() {
            taskListContainer.innerHTML = '';
            taskList.forEach(task => {
                const taskItem = document.createElement('li');
                taskItem.classList.add('task-item');
                taskItem.innerHTML = `
                    <strong>${task.name}</strong>
                    <div class="task-info">
                        Started at: ${task.startTime.toLocaleTimeString()} 
                        - End at: ${task.endTime.toLocaleTimeString()} 
                        - Duration: ${task.duration} min
                    </div>
                `;
                taskListContainer.appendChild(taskItem);
            });
        }

        startTaskButton.addEventListener('click', startTask);
    </script>
</body>
</html>
