# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
The header was "🎮 Game Glitch Investigator. An AI-generated guessing game. Something is off." The left side gives the user a choice of difficulty to choose from. They are easy, normal, and hard with normal difficulty being the defaulty setting. There is also a Developer Debug Info box to show us the developer the secret number, attempts made, score, and history of guesses. At the bottom is space to enter your guess. Underneath that is New Game button, Submut Guess button, and Show hint button which is turned on by default.
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").
  1. User can input non-integers and numbers outside of the described range.
  2. The New Game button did not work.

**Bug Reproduction Log**

Document at least 3 bugs you found. Add rows as needed.

| Input | Expected Behavior | Actual Behavior | Console Output / Error |
|-------|-------------------|-----------------|------------------------|
| -1 | Error: Input valid number | Program stopped working| Unable to put more guesses|
| Click the New Game Button | New instance of the game is activated | The game freezes and unable to start a new game | Program freezes and needs to restart|
| Secret number 50 and input 60 | Go lower message | Go higher message| No error message. Need to change the code.|

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
Claude. Specifically, the Haiku model.  

- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result). 

It helped to correct the number range bug. Claude was able to make it where non-integer numbers and numbers outside the described number range will not count towards the users' guesses and then ask for a valid number. Before implementing the change I asked Claude to describe the changes and then implement them. After further testing to see if any bugs appeared, I committed the code to GitHub. 

- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result). 

When the AI helped correct the New Game bug, it did not update the score to 0 with every new game instance. Yet, it updated everything else and did not tell me about the score bug. It was only after I tested the game, I found the score did not update to 0 when I pressed the New Game button. With the newfound information, I had Claude fix the bug. 

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed? 

I kept trying different test cases to see if the bug would reappear. I would try out a feature about 3 times using different test cases and situations to see if the bug would pop up again. After confirming the bug does not reappear, I move on to the next one. 

- Describe at least one test you ran (manual or using pytest) and what it showed you about your code. 

A test I tried towards the end suggested by Claude was to check if 1 and 100 work correctly. When I tried 1, it worked correctly, yet 100 showed a bug. It would flip between go higher and go lower when it should always say go lower unless the secret number is 100. When I pointed out the code failed at inputting 100, Claude was able to fix the bug. Showing me hidden bugs can and will live in my code unless test cases are done. 

- Did AI help you design or understand any tests? How? 
Yes, it helped me understand the methods used and how they interact with each other. Especially how the tests can find bugs and correct them. As for design AI was able to show how the method bodies can interact with one another to create a Streamlit instance.

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
Python’s Streamlit allows the language to bypass the usage of other backend routes such as HTML, CSS, and JavaScript. Instead, Python runs the program from the first line to the last line. This causes an issue as whenever a user interacts with any component of the program, Python must start the program from the first line to last line. This continues no matter which component of the program the user interacts with. Session state fixes the issue of Python constantly re-running the program. It achieves that by acting as a persistent memory that would run as the Python program re-runs. This allows the application to remember user input and updated variables. 


---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects? 

To hit one bug at a time. If I tell AI to fix multiple bugs at once, 1. token usage will skyrocket, and 2. AI can potentially re-write methods that would achieve different objectives. By focusing on one bug at a time, AI can be fine-tuned to solve issues. 

- This could be a testing habit, a prompting strategy, or a way you used Git. 

A main Git habit I’m starting to form is to commit small changes along with comments to explain why I decided to change the code. This is allowing to containerize Git commits to be able to reflect in the future. 

- What is one thing you would do differently next time you work with AI on a coding task? 

I must be more exact in my language when describing a problem. An example being to fix the restart button bug. After accepting a Claude edit to fix the bug, I ran into another issue where the score did not update. Without testing the code after editing it, I would have unknowingly let a bug run rampant. 

- In one or two sentences, describe how this project changed the way you think about AI generated code. 

AI needs a heavy hand in guidance to get the correct answer. On top of that, you must double check AI’s code as it can potentially ignore certain requests. Giving you the illusion of having fixed the bug when it spurred a new bug. 
