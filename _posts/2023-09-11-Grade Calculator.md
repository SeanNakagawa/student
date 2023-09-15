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
    <section>
        <h3>
            Total: <span id="total">0.0</span>
            Count: <span id="count">0.0</span>
            Average: <span id="average">0.0</span>
        </h3>
        <div id="scores">
            <!-- JavaScript-generated input boxes will appear here -->
        </div>
    </section>
    <script>
        // Function to create a new input box
        function newInputLine(index) {
            const scoresDiv = document.getElementById("scores");
            // Create and append a label for each score element
            const title = document.createElement('label');
            title.setAttribute('for', index);
            title.textContent = index + ". ";
            scoresDiv.appendChild(title);
            // Create and configure the score input element
            const score = document.createElement("input");
            score.setAttribute('id', index);
            score.setAttribute('type', "number");
            score.setAttribute('name', "score");
            score.setAttribute('style', "text-align: right; width: 5em");
            score.setAttribute('onkeydown', "calculator(event)");
            scoresDiv.appendChild(score);
            // Create and append a line break after the input box
            const br = document.createElement("br");
            scoresDiv.appendChild(br);
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
                let total = 0;  // Running total
                let count = 0;  // Count of input elements with valid values
                for (let i = 0; i < scoreInputs.length; i++) {
                    const value = parseFloat(scoreInputs[i].value);
                    if (!isNaN(value)) {
                        total += value; // Add to running total
                        count++;
                    }
                }
                // Update totals
                document.getElementById('total').textContent = total.toFixed(2); // Show two decimals
                document.getElementById('count').textContent = count;
                document.getElementById('average').textContent = (count > 0) ? (total / count).toFixed(2) : "0.0";
                // Add a new input line if all array values are valid
                if (count === scoreInputs.length) {
                    newInputLine(count);
                }
            }
        }
        // Create the first input box on window load
        newInputLine(0);
    </script>
</body>
</html>