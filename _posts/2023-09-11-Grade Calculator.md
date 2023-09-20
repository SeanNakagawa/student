---
toc: true
comments: false
layout: post
title: Grade Calculator
description: Calculates your grade and total points given your individual grades
type: hacks
courses: { csse: {week: 4} }
---
 
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Grade Calculator</title>
    <style>
        /* Add your custom CSS styles here */
        #scores {
            margin-top: 20px;
        }
        label {
            margin-right: 5px;
        }
        input[type="number"] {
            text-align: right;
            width: 5em;
        }
    </style>
</head>
<body>
    <header>
        <h1>Grade Calculator</h1>
        <h2>Input scores, press tab to add each new number.</h2>
    </header>
    <table>
        <tr>
            <th>Total: <span id="total">0.0</span></th>
            <th>Count: <span id="count">0.0</span></th>
            <th>Average: <span id="average">0.0</span></th>
            <th>Median: <span id="median">0.0</span></th>
        </tr>
        <tbody id="scores">
            <!-- JavaScript-generated input boxes will appear here -->
        </tbody>
    </table>
    <script>
        // Function to create a new input box
        function newInputLine(index) {
            // Create and configure the score input element
            const score = document.createElement("input");
            score.setAttribute('id', `score${index}`);
            score.setAttribute('type', "number");
            score.setAttribute('name', "score");
            score.setAttribute('style', "text-align: right; width: 5em");
            score.setAttribute('onkeydown', "calculator(event)");
            // Append the new input box to the "scores" tbody
            const scoresTBody = document.getElementById("scores");
            const newRow = scoresTBody.insertRow();
            const cell = newRow.insertCell();
            cell.appendChild(score);
            // Set focus on the new input line
            score.focus();
        }
        // Function to handle events and calculate totals
        function calculator(event) {
            const key = event.key;
            // Check if the pressed key is the "Tab" key (key code 9) or "Enter" key (key code 13)
            if (key === "Tab" || key === "Enter") {
                event.preventDefault(); // Prevent default behavior (tabbing to the next element)
                const scoreInputs = document.getElementsByName('score');
                let scoresArray = []; // Array to store valid scores
                for (let i = 0; i < scoreInputs.length; i++) {
                    const value = parseFloat(scoreInputs[i].value);
                    if (!isNaN(value)) {
                        scoresArray.push(value); // Add valid scores to the array
                    }
                }
                 if (scoresArray.length > 0) {
                    // Calculate total
            let total = scoresArray.reduce((acc, current) => acc + current, 0);
            // Calculate average
            let average = total / scoresArray.length;
            // Calculate median
            scoresArray.sort((a, b) => a - b);
            let median;
            if (scoresArray.length % 2 === 0) {
                const mid1 = scoresArray[scoresArray.length / 2 - 1];
                const mid2 = scoresArray[scoresArray.length / 2];
                median = (mid1 + mid2) / 2;
            } else {
                median = scoresArray[Math.floor(scoresArray.length / 2)];
            }
                // Update totals and median
            document.getElementById('total').textContent = total.toFixed(2);
            document.getElementById('count').textContent = scoresArray.length;
            document.getElementById('average').textContent = average.toFixed(2);
            document.getElementById('median').textContent = median.toFixed(2);
        } else {
            // If there are no valid scores, reset all values to zero
            document.getElementById('total').textContent = "0.0";
            document.getElementById('count').textContent = "0.0";
            document.getElementById('average').textContent = "0.0";
            document.getElementById('median').textContent = "0.0";
        }
                // Add a new input line
                newInputLine(scoreInputs.length + 1);
            }
        }
        // Create the first input box on window load
        newInputLine(1);
    </script>
</body>
</html>
