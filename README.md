# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 The Situation

You asked an AI to build a simple "Number Guessing Game" using Streamlit.
It wrote the code, ran away, and now the game is unplayable. 

- You can't win.
- The hints lie to you.
- The secret number seems to have commitment issues.

## 🛠️ Setup

1. Install dependencies: `pip install -r requirements.txt`
2. Run the broken app: `python -m streamlit run app.py`

## 🕵️‍♂️ Your Mission

1. **Play the game.** Open the "Developer Debug Info" tab in the app to see the secret number. Try to win.
2. **Find the State Bug.** Why does the secret number change every time you click "Submit"? Ask ChatGPT: *"How do I keep a variable from resetting in Streamlit when I click a button?"*
3. **Fix the Logic.** The hints ("Higher/Lower") are wrong. Fix them.
4. **Refactor & Test.** - Move the logic into `logic_utils.py`.
   - Run `pytest` in your terminal.
   - Keep fixing until all tests pass!

## 📝 Document Your Experience

- [ ] Describe the game's purpose.
   1. The user is tasked to guess a number from a range of 1-100. There are 3 modes: easy, normal, and hard. Each mode has different amount of guesses the user can make. With every guess made within alloted amount of tries the user is given a hint whether to go higher or lower. Once the user guesses the number correctly they are told they have won and can try the game again.
- [ ] Detail which bugs you found.
   1. The hint given to go higher or lower is incorrect. The hint is telling the user to guess the opposite way. For example if the number is 50 and the user guesses 40 the program tells the user to guess lower. It should be guess higher.
   2. The user is able to guess any non-whole number outside of the range 1-100.
   3. Each difficulty level shows the user 1 less attempt than they should have. For example normal diffculty should have 8 guesses, but the program only allows 7 guesses.
   4. The user cannot restart the program after the game is won or lose by clicking the "New Game" button. Instead, the program freezes, forcing the user to manually restart the program.
   5. When the user clicks the Enter key, the program does not register the keystroke. Instead the user must manually click "Submit Guess 🚀" to have the program register the guess.
- [ ] Explain what fixes you applied.
   1. I switched where the "Too Low", "📉 Go LOWER!" and "Too High", "📈 Go HIGHER!" locations. It gives the user accurate assessment of where the guesses.
   2. Within the parse_guess method I inserted code that dynamically enters the lowest and highest number of the number range given for a difficulty level. Finally I had the program guess counter up by 1 if the guess is a valid integer within the given number range.
   3. Changed the st.session_state.attempts to equal 0 instead of 1.
   4. Added st.session_state.status = "playing" and st.session_state.history = [] to correctly restart the program when the user clicks on "New Game 🔁."
   5. I had the program register the Enter keystroke.

## 📸 Demo Walkthrough

Describe your fixed game in numbered steps so a reader can follow along without watching a video:

1. <!-- Describe this step -->
2. <!-- Describe this step -->
3. <!-- Describe this step -->
4. <!-- Describe this step -->
5. <!-- Add more steps as needed -->

**Screenshot** *(optional)*: <!-- Insert a screenshot of your fixed, winning game here -->

## 🧪 Test Results

```
# Paste your pytest output here, e.g.:
# pytest tests/
# ========================= X passed in 0.XXs =========================
```

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, describe the Enhanced UI changes here — a screenshot is optional]
