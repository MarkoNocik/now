# Задача 5

Да се направи To-Do апликација која ќе овозможи додавање на обврски. Ако не е внесено ништо, се појавува alert.
Треба да се овозможи и бришење на обврските од листата со кликање на копчето remove. 
Исто така треба да се имплементира и бројач кој ќе го брои бројот на активни обврски.

  ![](img/image1.png)

# Решение:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>To-Do List Manager</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f7f7f7;
        }

        h1 {
            text-align: center;
            color: #333;
        }

        #newTaskInput {
            width: calc(100% - 160px);
            padding: 8px;
            margin-bottom: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
            font-size: 16px;
        }

        #taskList {
            list-style-type: none;
            padding: 0;
        }

        li {
            margin-bottom: 10px;
            font-size: 18px;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }

        button {
            padding: 8px 15px;
            background-color: #4caf50;
            color: #fff;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            transition: background-color 0.3s;
        }

        button:hover {
            background-color: #45a049;
        }

        input[type="checkbox"] {
            margin-right: 10px;
            cursor: pointer;
        }
    </style>
</head>
<body>
<h1>To-Do List Manager</h1>
<input type="text" id="newTaskInput" placeholder="Enter new task">
<button onclick="addTask()">Add Task</button>
<br>
<p>Tasks: <span id="taskCounter">0</span></p>
<ul id="taskList">

</ul>

<script>

    function addTask() {
        let taskInput = document.getElementById("newTaskInput"); // се зема содржината која е внесена
        let taskName = taskInput.value;
        if (taskName.trim() === "") { // проверуваме дали нешто е внесено, во спротивно бараме повторно
            alert("Please enter a task!"); // да се внесе
            return;
        }
        let taskList = document.getElementById("taskList"); // ја земаме листата
        let li = document.createElement("li");
        li.innerHTML =  '<input type="checkbox">' + taskName + ' <button onclick="removeTask(this)">Remove</button>';//креираме
        // нов елемент кој ќе се додаде на листата
        taskList.appendChild(li); // го додаваме на листата
        taskInput.value = ""; // ја ресетираме вредноста

        updateTaskCounter();
    }

    function removeTask(button) {// функција за бришење на елемент од листата
        let listItem = button.parentNode; // го земаме елементот од листата
        listItem.parentNode.removeChild(listItem); // го бришеме
        updateTaskCounter();
    }
    function updateTaskCounter() { // функција која брои активни таскови
        let taskCounter = document.getElementById("taskCounter");
        let taskList = document.getElementById("taskList");
        taskCounter.textContent = taskList.children.length;
    }
</script>
</body>
</html>
```