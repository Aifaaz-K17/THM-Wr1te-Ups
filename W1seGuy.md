# TryHackMe — W1seGuy | Hint-Based Write-Up

**Difficulty:** Easy | **Category:** Cryptography
**Room link:** https://tryhackme.com/room/w1seguy

*Same deal as before — this is a nudge, not a shortcut. If you're reading this without having tried the room first, go try it. You'll get more out of it.*

---

## What's the Room About

The tagline on the room page is a hint in itself: *"A w1se guy 0nce said, the answer is usually as plain as day."* Read that again after you solve it and it'll make you laugh a little.

You're given two things: a Python source file, and a server running on port 1337. The server sends you an XOR-encrypted string in hex and then asks you for the encryption key. Give it the right key, and you get flag 2. Flag 1 is hiding in the encrypted string itself, once you actually decrypt it.

The whole room is built around one concept: XOR encryption. If you've never encountered XOR before, that's fine — but before you touch anything else, take ten minutes to understand what XOR actually does. Not just "it's a bitwise operator" but *why* it's so useful for encryption and, crucially, why it's trivially breakable under certain conditions. That understanding is what makes the rest click.

## Step 1 — Actually read the source code

Download the Python file from Task 1 and open it. Don't skim it — read it properly.

Three things you need to pull out of it:

First, what is the key? How long is it, and how is it generated? Pay attention to the character set.

Second, how exactly does the encryption work? Look at the line where the flag gets XOR'd with the key. Notice that the key is shorter than the flag — so what does the code do to handle that? That detail matters a lot.

Third, what does the server actually send you, and in what format? Hex? Raw bytes? This affects how you work with it later.

Once you understand those three things, you're already halfway there. The source code is the solution — it tells you everything you need to break it. That's by design.

---

## Step 2 — Connect to the Server

Use netcat to hit port 1337 on the machine IP. The server will spit out a hex string and ask for the key.

Copy that hex string somewhere. You're going to need it.

Don't guess the key at random. You don't have to.

---

## Step 3 — The Core Insight (Don't Skip This)

Here's the thing about XOR that makes this challenge solvable. If you XOR something with a key to encrypt it, you can XOR the encrypted result with the *same key* to get the original back. That's not a bug, it's just how XOR works mathematically.

Now here's the part that breaks this encryption scheme wide open: you already know part of the plaintext.

Every THM flag starts the same way. And the key in this challenge is only 5 characters long. So even before you know anything else, you can figure out several characters of the key immediately — just by XOR-ing the beginning of the encrypted hex with the characters you *know* must be at the start of the flag.

Work through that logic slowly if it doesn't land immediately. Write it out on paper if you need to. Once you see why it works, the rest is just execution.

You'll recover most of the key this way. Not all of it — you'll be one character short. But think about what you know about the *end* of a THM flag too. That last character isn't a mystery either.

---

## Step 4 — Two Ways to Finish This

Once you understand the approach, you've got options for actually executing it.

**CyberChef** is the easiest if you want to do this visually and interactively. It has an XOR operation built in. You can paste your hex string in, set the key to what you know so far, and play with it until the output starts looking like readable text. This is a good way to verify your thinking before you automate anything.

**Python** is the cleaner approach if you want to do it properly. You've already got the source code as a reference — writing a short script that recovers the key and decrypts the flag is genuinely good practice. It doesn't need to be long. You're looking at maybe 20-30 lines if you write it cleanly.

Either way works. If you're still learning, try CyberChef first just to see what's happening, then go back and write the Python version so you actually understand each step.

---

## Step 5 — Submit and Get Flag 2

Once you have the key, send it back to the server. If you've got the right one, the server will hand you flag 2.

Flag 1 you should already have at this point — it's the decrypted version of the hex string the server gave you.

---

## The Bit Worth Actually Thinking About

This room is flagged as "easy" and honestly, once you get the XOR insight, it is. But don't let that make you dismiss what it's teaching.

XOR encryption by itself is genuinely weak for exactly the reason this room demonstrates — if you know *anything* about the plaintext, you can start recovering the key. This is called a **known-plaintext attack**, and it's not some exotic theoretical thing. It's why nobody should be rolling their own encryption with XOR and a short static key, and it's why CTF challenges love using it as a teaching tool.

The bigger lesson: encryption schemes that look secure on the surface can fall apart completely the moment an attacker has even a tiny foothold of known data. And in practice, attackers often do — because formats, headers, and flag conventions give structure away for free.

If this room made you curious about cryptography properly, the rabbit hole is deep and worth going down. There's a reason crypto is its own discipline.

---

Good luck. The "aha" moment when the XOR logic clicks is genuinely satisfying — give yourself the chance to reach it on your own.
