# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
When I first ran the game, the interface loaded normally and showed the score, difficulty, and guess history, but the gameplay behaved incorrectly. The hints did not match my guesses—for example, the game told me to “Go Higher” even when my guess was already above the secret number. The score also dropped into negative values very quickly, which showed that the scoring logic was broken. Additionally, the game ended early after only six attempts instead of allowing the full eight guesses. Overall, the game looked functional on the surface, but several core mechanics were clearly malfunctioning.
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").

**Bug Reproduction Log**

Document at least 3 bugs you found. Add rows as needed.

| Input | Expected Behavior | Actual Behavior | Console Output / Error |
|-------|-------------------|-----------------|------------------------|
| 69    |     Go lower           Go higher           None
| 96    |    Score= -5 point|Score =-10 points| showed wrong score number
|6 attempts | allow 8 inputs | allowed only 6 inputs | game over

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
  I used GitHub Copilot as an AI teammate. I asked it to inspect the guessing logic, explain the check_guess function, and identify why the hints, score, and attempts were incorrect.
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
 Copilot correctly suggested that the hint messages were reversed: a “Too High” guess should say “Go LOWER,” while a “Too Low” guess should say “Go HIGHER.” I verified this by tracing the if guess > secret and else branches with test values such as 69 and 50.
- Give one example of an AI suggestion you did not accept as written (including what the AI suggested, why you rejected or changed it, and how you verified your version). It does not have to be a suggestion that was wrong: over-engineered, out of scope, harder to read, or a poor fit for this codebase all count.
Copilot identified that converting the secret number to a string could cause incorrect comparisons. I did not keep that string-based approach because comparing values like "69" and "100" alphabetically does not work like numeric comparison. I kept the values numeric and verified the logic by checking that guesses above the secret produce “Go LOWER” and guesses below it produce “Go HIGHER."
---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
I decided a bug was fixed by reproducing the original problem and checking the result against the expected behavior. For example, I tested a guess above the secret and confirmed that the game displayed “Go LOWER,” while a guess below the secret displayed “Go HIGHER.” I also started a new game to check that the attempts, score, and history reset correctly, and I checked each difficulty to confirm that its number range was used.
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
I ran the game manually with guesses such as 69 and 50, and I checked the winning case where both the guess and secret were 3. These checks showed that the comparison and hint logic worked correctly after the fix. I also prepared pytest tests for winning, too-high, and too-low guesses; the direct `pytest` command could not run because pytest was not available on the terminal PATH, so I did not treat that command as a successful test result.
- Did AI help you design or understand any tests? How?
Yes, Copilot helped me understand which boundary cases to test by explaining the `check_guess` branches. It suggested checking equal values, guesses above the secret, and guesses below the secret. I used those cases to verify both the returned outcome and the displayed hint, rather than testing only the winning path.

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
Streamlit reruns the Python script from top to bottom whenever a user interacts with a widget, such as clicking a button. Normal variables can be recreated during each rerun, so values that need to persist, such as the secret number, attempts, score, and history, belong in `st.session_state`. I learned that session state acts like a small storage area for one user's game, which keeps the game from losing its progress after every click.

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.

One habit I want to reuse is reproducing a bug with a small, specific input before changing the code. I will write down the expected and actual behavior, then test the same case again after the fix. This makes it easier to tell whether the change solved the original problem instead of only changing the symptoms.
- What is one thing you would do differently next time you work with AI on a coding task?

Next time, I would ask the AI to explain the relevant code before accepting a proposed fix. I would also run the tests immediately after each small change instead of waiting until several changes were complete. This would help me catch incorrect assumptions and environment problems earlier.
- In one or two sentences, describe how this project changed the way you think about AI generated code.

This project showed me that AI-generated code can look complete while still containing bugs in basic logic and state management. I now see AI as a useful debugging partner, but I know I must inspect its reasoning, test its suggestions, and make the final decisions myself.
