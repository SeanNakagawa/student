---
toc: true
comments: false
layout: post
title: Number Game
description: Guess the number!
type: hacks
courses: { csse: {week: 3} }
---
 
# Guess the Number

Guess the number 1-100

<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Guess the Number Game</title>
  <style>
    /* Add some CSS styling here if needed */
  </style>
</head>
<body>

<div class="game-container">
  <h1>Guess the Number Game</h1>
  <p>Try to guess the number between 1 and 100.</p>

  <details>
    <summary>Guess the Number Input</summary>

    <div class="input-container">
      <input type="text" id="guessInput" placeholder="Enter your guess...">
      <button onclick="checkGuess()">Submit</button>
    </div>

    <p id="message"></p>
  </details>
</div>

<script>
  // JavaScript code to handle the game logic
  const randomNumber = Math.floor(Math.random() * 100) + 1;
  let attempts = 0;

  function checkGuess() {
    const guess = parseInt(document.getElementById("guessInput").value);
    attempts++;

    if (guess === randomNumber) {
      document.getElementById("message").innerHTML = `Congratulations! You correctly guessed the number (${randomNumber}) in ${attempts} attempts.`;
    } else if (guess < randomNumber) {
      document.getElementById("message").innerHTML = "Too low! Try again.";
    } else {
      document.getElementById("message").innerHTML = "Too high! Try again.";
    }
  }
</script>

</body>
</html>
