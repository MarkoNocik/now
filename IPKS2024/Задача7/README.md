# Задача 7

Потребно е да се креира калкулатор кој пресметува плата
Се внесуваат името, часовите и саатницата (hourlyRate) кој ги работел вработениот.
Потребно е да се внесат сите параметри, во спротивно излегува alert.
Потребно е да се направи пресметка за платата на вработениот според *(бројот на часови &times; саатницата)*
Во зависност од платата се менуваат параметрите за најмногу платен вработен и најмалку платен вработен
На почетокот нема да има ни најмалку платен ни најмногу платен вработен. 
Потребно е да се ресетираат вредностите по внес.

  ![](img/image1.png)

# Решение:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Employee Salary Calculator</title>
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

        form {
            max-width: 400px;
            margin: 0 auto;
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }

        input[type="text"],
        input[type="number"] {
            width: calc(100% - 12px);
            padding: 8px;
            margin-bottom: 15px;
            border: 1px solid #ccc;
            border-radius: 4px;
            font-size: 16px;
        }

        button {
            display: block;
            width: 100%;
            padding: 10px;
            background-color: #4caf50;
            color: #fff;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }

        button:hover {
            background-color: #45a049;
        }

        .result {
            margin-top: 20px;
        }

        h2 {
            margin-top: 20px;
            color: #333;
        }

        p {
            margin: 5px 0;
        }
    </style>
</head>
<body>
<h1>Калкулатор на заработка</h1>
<form>
    <div>
        <label for="employeeName">Име на вработениот:</label>
        <input type="text" id="employeeName" required>
    </div>
    <div>
        <label for="hoursWorked">Часови на работа:</label>
        <input type="number" id="hoursWorked" required>
    </div>
    <div>
        <label for="hourlyRate">Саатница:</label>
        <input type="number" id="hourlyRate" required>
    </div>
    <button type="button" onclick="calculateSalary()">Калкулирајте заработка</button>
</form>
<div class="result">
    <h2>Највисоко платен вработен:</h2>
    <p id="highestPaid">Нема податоци</p>
    <h2>Најниско платен вработен:</h2>
    <p id="lowestPaid">Нема податоци</p>
</div>

<script>

    function calculateSalary() {
        const employeeNameInput = document.getElementById("employeeName"); // земање на вредностите
        const hoursWorkedInput = document.getElementById("hoursWorked"); // внесени од корисникот
        const hourlyRateInput = document.getElementById("hourlyRate"); 
        const employeeName = employeeNameInput.value;
        const hoursWorked = parseFloat(hoursWorkedInput.value);
        const hourlyRate = parseFloat(hourlyRateInput.value);

        if (!employeeName || isNaN(hoursWorked) || isNaN(hourlyRate)) { // проверување дали е се внесено
            alert("Внесете валидни податоци!");
            return;
        }
       

        const salary = hoursWorked * hourlyRate; // пресметка за плата

        const highestPaidElement = document.getElementById("highestPaid");
        const lowestPaidElement = document.getElementById("lowestPaid");

        if (highestPaidElement.textContent === "Нема податоци") { // ако случај да е празно полето
            highestPaidElement.textContent = `${employeeName}: $${salary}`; // се става името на вработениот и платата
            lowestPaidElement.textContent = `${employeeName}: $${salary}`;
        } else {
            const highestPaidText = highestPaidElement.textContent.split(": ");
            const lowestPaidText = lowestPaidElement.textContent.split(": ");
            const currentHighestSalary = parseFloat(highestPaidText[1].slice(1));
            const currentLowestSalary = parseFloat(lowestPaidText[1].slice(1));

            if (salary > currentHighestSalary) { // се проверува дали претходната плата е поголема од
                // таа која е внесена сега
                highestPaidElement.textContent = `${employeeName}: $${salary}`;
            }
            if (salary < currentLowestSalary) {// се проверува дали претходната плата е помала од
                // таа која е внесена сега
                lowestPaidElement.textContent = `${employeeName}: $${salary}`;
            }
        }

        employeeNameInput.value = ""; // се ресетираат вредностите
        hoursWorkedInput.value = "";
        hourlyRateInput.value = "";
    }
</script>
</body>
</html>
```