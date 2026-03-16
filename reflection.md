# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
It took a long time to load 
- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").
  - the new game button isn't functioning properly
  - the hint gives the opposite number 
  -  Attempts left showed a negative number
  - the normal has a higher range compared to the hard





---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
Claude and Copilot

- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
The issue is in the "New Game" button logic in app When clicked, it resets st.session_state.attempts to 0 and generates a new secret using random.randint(1, 100), which is hardcoded and ignores the selected difficulty.
Fix: update the line to use the difficulty range:
st.session_state.secret = random.randint(low, high)

I verified this suggestion by reviewing the code and confirming that low and high correspond to the difficulty range selected by the user

- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).
i think one incorrect suggestion from the AI involved the TypeError handling in the check_guess function. The AI suggested removing the try/except block.
---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
By testing it on pytest and playing the game 
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
  tested the New Game button and observed that the attempts counter and score were not fully resetting. This helped me identify that several session state values (such as status, history, and score) needed to be reset when starting a new game.
- Did AI help you design or understand any tests? How?
Yes they did help me to design the test and also explaining how Streamlit reruns work, which made it easier to understand why certain bugs were happening.
---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
The secret number kept changing because Streamlit reruns the entire script every time the user interacts with the app

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
Streamlit works by rerunning the whole program every time something changes on the page. Session state is like a small storage box that keeps important values even when the app reruns.
- What change did you make that finally gave the game a stable secret number?
The change that fixed the issue was storing the secret number in st.session_state.secret and only generating it when the value does not already exist.
---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
  The developer debug section that displayed the secret number, attempts, score, and history made it much easier to understand what the program was doing internally. This kind of visibility helps identify bugs faster.

- What is one thing you would do differently next time you work with AI on a coding task?
I would spend more time reviewing and testing the AI-generated code before assuming it is correct.

- In one or two sentences, describe how this project changed the way you think about AI generated code.
AI-generated code can be very helpful for speeding up development, but it should never be trusted without testing. human in the loop!
