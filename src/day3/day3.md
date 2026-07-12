## Open-Ended Tasks

You've built a working chatbot. Now make it _yours_. None of these activities are mandatory, but they should provide a solid challenge for those who have managed to get their bot up and working.

> **How to read the difficulty markers**
> 🟢 Easy · 🟡 Medium · 🔴 Hard
>
> Each task has a **Goal**, some **Hints**, and a **Done when…** line so you know when to stop tinkering and move on. 

---

## Task 1 · Explore the API 🟢

**Goal:** Understand what knobs the API gives you, and feel how each one changes our chatbots's replies.

The official reference is your friend here:

- API overview → <https://docs.claude.com/en/api/overview>
- Messages API reference (all request parameters) → linked from the overview

Right now your request only sends `model`, `max_tokens`, `system`, and `messages`. Try adding and adjusting these in the `json={...}` block of `get_ai_reply`:

| Parameter        | What it does                             | Try                                                                    |
| ---------------- | ---------------------------------------- | ---------------------------------------------------------------------- |
| `max_tokens`     | Caps how long the reply can be           | Set it very low (e.g. `30`) and watch replies get cut off mid sentence |
| `temperature`    | Randomness / "creativity", `0.0`–`1.0`   | Ask the same question at `0.0` vs `1.0` a few times and compare        |
| `system`         | Sets the chatbots's role and personality | Rewrite it as a pirate, or even compclub mentor                        |
| `stop_sequences` | Text that makes the chatbot stop early   | Give it `["\n\n"]` and see what happens                                |

> [!SUCCESS] Done when...
> You can explain to a mentor what `temperature`, `max_tokens`, and the `system` parameters do, in one sentence each

---

## Task 2 · Add Non-AI Commands 🟡

**Goal:** Let the user type special commands that the server handles _itself_, without calling the chatbot. Start with `/clear` to reset the conversation.

**Hints:**

- Handle this in the backend, inside your `/api/chat` route, **before** you call `get_ai_reply`.
- Check the incoming message: if it starts with `/` (or `./`), treat it as a command instead of a prompt.

```python
if user_message.strip() == "/clear":
    conversation.clear()
    return jsonify({"reply": "🧹 Conversation cleared."})
```

- Once `/clear` works, add more: `/help` (list commands), `/system <text>` (change the system prompt on the fly), `/undo` (remove the last exchange).

> [!SUCCESS] Done when...
> Typing `/clear` empties the history, and the website reflects this functionality

---

## Task 3 · Persistent Memory (Save to a File) 🟡

**Goal:** Right now, restarting the server wipes the bot's memory. Fix that by saving the conversation to a file and loading it back on startup.

**Hints:**

- The `conversation` list is just data you can dump it to JSON.

```python
import json

HISTORY_FILE = "history.json"

def save_history():
    with open(HISTORY_FILE, "w") as f:
        json.dump(conversation, f)

def load_history():
    try:
        with open(HISTORY_FILE) as f:
            return json.load(f)
    except FileNotFoundError:
        return []

conversation = load_history()
```

- Call `save_history()` **after** you append the assistant's reply (and after `/clear`).
- Handle the case when there is no file (first save)

> [!SUCCESS] Done when...
> You can tell the bot to remember a specific word (for example pineapple), restart the server, and have the bot remember the word

---

## Task 4 · Trim Conversation Automatically 🔴

**Goal:** Long conversations cost more tokens and eventually overflow the model's context. Set a maximum memory size and trim old messages automatically when you exceed it.

Note: you may want to add in a new "/" command that prints the saved chatlog history for the purposes of debugging this.

**Hints:**

- Decide your limit as a number of _messages_ (each user/assistant turn is one entry), e.g. keep the most recent 20.
- Trim from the **front** (oldest first):

```python
MAX_MESSAGES = 20

def trim_history():
    while len(conversation) > MAX_MESSAGES:
        conversation.pop(0)
```

> [!SUCCESS] Done when...
> A veeeeeerryyyyyy long conversation is automatically trimmed

---

## Extra Extension Ideas

> [!NOTE] Note
> Some of these are fairly difficuly and may require editing our website itself. Please feel free to ask mentors for help with them if you feel stuck or unsure where to start.

> [!NOTE] Another Note!
> Feel free to complete them in any order! However, some may be easier with previous tasks done first - ask mentors for guidance!

Our slides on HTML & CSS: [slides link](https://docs.google.com/presentation/d/1cv2NICfhln9tCqrtoX2xc99DpvEw4a-ZpKdcE2WuY6s/edit?usp=sharing)

HTML: [https://www.w3schools.com/html/](https://www.w3schools.com/html/)

CSS: [https://www.w3schools.com/Css/](https://www.w3schools.com/Css/)

- **🟢 Timestamps** on each message bubble in the UI.
- **🟡 Personality switcher** — a dropdown or `/persona` command that swaps between several system prompts.
- **🟡 Export the chat** — a button that downloads the conversation as a `.txt` or `.md` file.
- **🟡 Loading indicator** — show a "chatbot is typing…" bubble while you wait for the reply.
- **🟡 Edit Messages** - allow messages in your chat to be edited after they've been sent (no need to regenerate existing AI replies)
- **🟡 Show Token Counts** - explore the Claude API and see which request parameters you can use to get data on how many tokens each message, and the whole conversation, is using. I wonder if we could see how much of our conversation context we've used too...
- **🔴 Delete Messages** - allow messages to be deleted in your chat. Once a message has been deleted, everything after that message (user requests and AI responses) should also be deleted
- **🔴 Multiple Separate Chats** — give each conversation an ID so one user can keep several concurrent conversations
- **🔴 Group Conversations** - allow conversations to be grouped into folders
- **🔴🔴🔴 Branching Chats (if you dare)** - duplicate an existing chat, up to a certain message.
---

## Appendix

### Installing Python Packages

If you need to install some Python packages, then you can use the below commands to get that sorted.
> [!WARNING] Warning!!
> Before you install ANYTHING, get a mentor to take a look at the package

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### Debugging Your Code

- Step 1: Check if your code is indented properly!
- Step 2: ask for help!
    - Hint: try reading the error message to see what line in your code is causing the error

---
