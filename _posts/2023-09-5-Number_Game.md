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

<details>
  <summary>Guess the Number Input</summary>

  <!-- Replace this with your own input field code if you have a web page or platform to host it -->
  <input type="text" id="guessInput" placeholder="Enter your guess...">
  <button onclick="checkGuess()">Submit</button>

  <p id="message"></p>
</details>

<script>
  // JavaScript code to handle the game logic
  const randomNumber = Math.floor(Math.random() * 100) + 1;
  let attempts = 20;

  function checkGuess() {
    const guess = parseInt(document.getElementById("guessInput").value);
    attempts++;

    if (guess === randomNumber) {
      document.getElementById("message").innerHTML = `You did it! You correctly guessed the number! ${randomNumber} in ${attempts} attempts.`;
    } else if (guess < randomNumber) {
      document.getElementById("message").innerHTML = "Too low! Try again.";
    } else {
      document.getElementById("message").innerHTML = "Too high! Try again.";
    }
  }
</script>
