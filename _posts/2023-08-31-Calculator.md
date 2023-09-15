---
toc: true
comments: false
layout: post
title: Basic Calculator
description: Basic Calculator Test 
type: hacks
courses: { csse: {week: 2} }
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculator</title>
    <style>
        /* Styling for the calculator container */
        .calculator {
            width: 300px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f0f0f0;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.2);
        }
        #display {
            width: 100%;
            height: 50px;
            font-size: 24px;
            text-align: right;
            margin-bottom: 10px;
            padding: 5px;
            border: none;
            border-radius: 5px;
        }
        .button-container {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 5px;
        }
        .button {
            width: 50px;
            height: 50px;
            font-size: 18px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            background-color: #337ab7;
            color: #fff;
        }
        #equals {
            background-color: #5cb85c;
        }
        #clear {
            background-color: #d9534f;
        }
        .button:hover {
            background-color: #286090;
        }
    </style>
</head>
<body>
<div class="calculator">
    <h1>Calculator</h1>
    <input type="text" id="display" readonly>
    <div class="button-container">
        <button class="button" onclick="appendToDisplay('1')">1</button>
        <button class="button" onclick="appendToDisplay('2')">2</button>
        <button class="button" onclick="appendToDisplay('3')">3</button>
        <button class="button" onclick="appendToDisplay('+')">+</button>
        <button class="button" onclick="appendToDisplay('4')">4</button>
        <button class="button" onclick="appendToDisplay('5')">5</button>
        <button class="button" onclick="appendToDisplay('6')">6</button>
        <button class="button" onclick="appendToDisplay('-')">-</button>
        <button class="button" onclick="appendToDisplay('7')">7</button>
        <button class="button" onclick="appendToDisplay('8')">8</button>
        <button class="button" onclick="appendToDisplay('9')">9</button>
        <button class="button" onclick="appendToDisplay('*')">*</button>
        <button class="button" onclick="appendToDisplay('0')">0</button>
        <button id="clear" onclick="clearDisplay()">C</button>
        <button id="equals" onclick="calculate()">=</button>
        <button class="button" onclick="appendToDisplay('/')">/</button>
    </div>
</div>

<script>
    function appendToDisplay(value) {
        document.getElementById("display").value += value;
    }

    function clearDisplay() {
        document.getElementById("display").value = "";
    }

    function calculate() {
        try {
            const result = eval(document.getElementById("display").value);
            document.getElementById("display").value = result;
        } catch (error) {
            document.getElementById("display").value = "Error";
        }
    }
    document.addEventListener("keydown", function (event) {
        const key = event.key;

        // Allow digits, operators, and common keys like Enter and Backspace
        if (/[\d+\-*/.Cce=]|Enter|Backspace|Escape/.test(key)) {
            if (key === "Enter") {
                calculate();
            } else if (key === "C" || key === "c" || key === "Escape" || key === "Backspace") {
                clearDisplay();
            } else {
                appendToDisplay(key);
            }
            event.preventDefault(); // Prevent default behavior for the pressed key
        }
    });
</script>
</body>
</html>
