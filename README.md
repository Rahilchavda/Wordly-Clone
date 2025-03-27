# Wordly-Clone
Covid era games !
🎯 Wordle Clone with React & Tailwind
A simple Wordle Clone built with React, Tailwind CSS, and useState/useEffect hooks. This project implements core game logic, user input handling, and tile coloring to mimic the classic Wordle experience.

🚀 Features
✅ Fetch Wordle Word List – Retrieves a list of valid Wordle words from an API
✅ Random Word Selection – Picks a random word as the solution
✅ Dynamic Board Rendering – Displays a 6-row game board for guesses
✅ User Input Handling – Detects keyboard input and updates the board dynamically
✅ Guess Validation – Checks if a guess is valid before submission
✅ Win/Loss Detection – Ends the game if the correct word is guessed
✅ Tile Coloring System – Highlights tiles as correct (green), close (yellow), or incorrect (gray)

📌 Implementation Steps
1️⃣ Fetching the Word List & Setting Up the Board
Fetch the list of Wordle words from:

ruby
Copy
Edit
https://api.frontendexpert.io/api/fe/wordle-words
Select a random word and store it in the randomWord constant

Use useState to store solution and update it with setSolution(randomWord)

Use useEffect to call the fetchWord function when the component mounts

Create a guesses state array with 6 slots, initially set to null

Render the board inside a <div>, mapping guesses to the <Line> component

2️⃣ Rendering the Game Board
The Line component:

Initializes an empty tiles array

Loops through the guess characters

Pushes each character inside a <div> with the class tile

Returns the final rendered tiles

3️⃣ Handling Keyboard Input
Use useEffect to listen for key presses

Attach an event listener (keydown) to trigger handleType

Remove the listener when the component unmounts

handleType(event):

Identifies the key pressed

Updates currentGuess dynamically

Uses functional updates (oldGuess => ...) to optimize performance

4️⃣ Submitting & Validating Guesses
Handle Enter Key Press:

Checks if currentGuess.length === 5

Submits the guess if valid

If correct, sets isGameOver = true

If incorrect, moves to the next row

Handle Backspace:

Deletes the last character from currentGuess

5️⃣ Changing Tile Colors Based on Guess Accuracy
Adding isFinal in Line:

A guess is "final" if it's not the current guess and is not null

Only final guesses can change colors

Checking Correctness:

Green 🟩 (Correct) – char === solution[i]

Yellow 🟨 (Close) – char exists in solution but at a different position

Gray ⬜ (Incorrect) – char is not in solution

Update CSS for Styling:

Add Tailwind classes dynamically for tile colors

6️⃣ Handling Letter Input with Regex
Ensure only valid letters (a-z) are accepted

Use event.key.match(/^[a-z]$/) to validate input

🎨 UI Styling (Tailwind CSS)
Feature	Tailwind Class Used
Board Layout	flex flex-col items-center gap-2
Tiles	w-[50px] h-[50px] border flex items-center justify-center text-xl font-bold
Correct Guess	bg-green-500 text-white
Close Guess	bg-yellow-500 text-black
Incorrect Guess	bg-gray-400 text-white
💻 Running the Project
Backend Setup (Proxy Server)
Create a server.js file:

js
Copy
Edit
const express = require("express");
const cors = require("cors");
const fetch = (...args) => import('node-fetch').then(({ default: fetch }) => fetch(...args));

const app = express();
app.use(cors());

const API_URL = "https://api.frontendexpert.io/api/fe/wordle-words";

app.get("/proxy", async (req, res) => {
    try {
        const response = await fetch(API_URL);
        const data = await response.json();
        res.json(data);
    } catch (error) {
        console.error("Error fetching data:", error);
        res.status(500).json({ error: "Failed to fetch data" });
    }
});

app.listen(5001, () => console.log("✅ Backend running on port 5001"));
Run the backend:

bash
Copy
Edit
node server.js
Frontend Setup
Install dependencies:

bash
Copy
Edit
npm install
Start the React App:

bash
Copy
Edit
npm start
📜 License
This project is open-source under the MIT License.

📩 Contact
For any questions or suggestions, feel free to reach out! 🚀

This README is structured, well-formatted, and easy to follow. Let me know if you need any modifications! 😊
