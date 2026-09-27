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

- [x] Describe the game's purpose.
- [x] Detail which bugs you found.
- [x] Explain what fixes you applied.

The game's purpose is to let a player guess a randomly selected number within a difficulty-based range. The game gives higher or lower hints, tracks attempts and score, and records the guess history. I found that the hints were backwards, string comparisons could produce incorrect results, the score could change incorrectly or become negative, attempts started at the wrong value, and a new game did not reset all state. I fixed these problems by keeping comparisons numeric, moving the helper logic into `logic_utils.py`, making scoring consistent and nonnegative, starting attempts at zero, using the selected difficulty range, and resetting the complete session state for a new game.

## Demo Walkthrough

1. The game starts with the secret stored in session state, zero attempts, a zero score, and an empty history.
2. The user enters `40` when the secret is `60`, and the game returns `Too Low` with the hint `Go HIGHER!`.
3. The user enters `70`, and the game returns `Too High` with the hint `Go LOWER!`.
4. The score decreases by five points for each incorrect guess but never becomes negative, and both guesses appear in the history.
5. The user enters `60`, the game returns `Correct!`, awards the win score, and ends the round.
6. Selecting New Game resets the secret, attempts, score, status, and history so another round starts cleanly.

## 🧪 Test Results

The regular game-logic test suite passed. The optional Challenge 1 advanced edge-case tests were not completed.

```text
> .\.venv\Scripts\python.exe -m pytest tests
============================= test session starts =============================
platform win32 -- Python 3.14.0, pytest-9.1.1, pluggy-1.6.0
collected 3 items

tests\test_game_logic.py ...                                             [100%]

============================== 3 passed in 0.03s ==============================
```

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, describe the Enhanced UI changes here — a screenshot is optional]
