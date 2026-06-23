# TryHackMe — ContAInment | Hint-Based Write-Up

**Difficulty:** Medium | **Category:** AI Security / DFIR
**Room link:** https://tryhackme.com/room/containment

*Heads up — this guide won't hand you answers. It's meant to nudge you in the right direction when you're stuck, not to do the room for you. If you're here after genuinely hitting a wall, that's exactly what this is for.*

---

## What's Going On (the story)

So the premise here is that you're a security analyst at West Tech — some kind of defence R&D contractor. One of their senior researchers, Oliver Deer, has had his workstation flagged for weird network activity. By the time anyone noticed, there was already a ransom note sitting on his desktop.

The job: figure out how the attacker got in, what they did, and claw back whatever you can.

What makes this room different from your standard DFIR challenge is that you're not doing it alone. There's an AI incident response assistant running locally on the box, and it's not just decoration — it's got actual tools and you'll need to actually use it. If you've been ignoring it, go back. It's the point.

---

## Getting Started

SSH in with the credentials from the room page. Nothing fancy here — once you're on the machine, just do what any analyst would: look around.

Run `ls` in the home directory. Don't rush past this step. Take a minute to actually read what's there, because something will seem a bit out of place for a researcher's account. What files would *you* not expect to see sitting in a normal user's home folder?

---

## Step 1 — Finding the PCAPs

Somewhere on this machine there are packet capture files. These are your best shot at reconstructing what the attacker actually did on the network.

You want to find all `.pcap` files under the user's home directory. Think about how you'd do that — there's a tool built into Linux that's perfect for searching by filename recursively. Once you run it, you'll get back a list that spans a few date-named subdirectories.

> **Stuck?** The command structure you want is `find [starting path] -type f -name "*.pcap"`. After that, just read through what comes back.

---

## Step 2 — Which PCAP Actually Matters

Here's where a lot of people waste time — they try to open everything. Don't do that.

You've got multiple captures across multiple dates. Most of them are going to be boring. So before you start digging into any of them, think about two things:

First, **file size**. If you `ls -la` inside each directory, you'll notice that most captures are roughly the same size. One of them isn't. That anomaly is what you want.

Second, **the filename itself**. Attacker tools often default to well-known ports. If you see a port number in one of those filenames that you'd normally associate with remote access or shells, that's not a coincidence.

You shouldn't need to check every file. The right one should stick out pretty quickly once you look at it this way.

---

## Step 3 — Let the AI Do Some Heavy Lifting

Alright — you've got your suspicious PCAP. Now open up the AI assistant interface in your browser (it's running on port 7860).

Tell it what you're trying to do. You don't need to speak in commands or remember any syntax — just describe the situation. Something like "I have a pcap file at this path, can you reassemble the data from it" is enough. The assistant has tools for exactly this kind of thing and it'll figure out what to invoke.

Once it's done, it saves output somewhere on the local filesystem. Before you ask where — think about the AI model that's running on this machine. Its name will give you a clue about the output folder name.

Go find that folder and read what's in it.

---

## Step 4 — Reading the Attacker's Own Notes

The reassembled output is going to look messy at first. That's okay. Read it carefully rather than skimming.

What you're hunting for:

- Evidence of *how* the attacker tried to manipulate the AI system. This is actually the most interesting part of the room conceptually — there's a well-known attack technique against LLMs buried in here.
- Any strings that look like credentials or passphrases. Attackers are not always as careful as they think they are, and this one left something behind they probably didn't mean to.
- Anything that reads like notes-to-self.

If you spot something that looks like a password, write it down. You'll need it in a moment.

---

## Step 5 — Cracking Open the Zip

Remember that unusual file sitting in the home directory back when you first looked around? Time to use it.

Run `unzip` on it. It'll ask for a password. If you found the right string in the output from the last step, this will work first try. If it doesn't, go back and look again — you may have grabbed the wrong thing.

Once it opens, look at what's inside.

---

## Step 6 — The Flag Is in There, But Not Alone

Inside the archive you'll find a mix of project files and one file that's clearly flag-related. The catch is that it doesn't just contain one candidate — there are several encoded strings in there, and only one of them is the real flag.

They're encoded in a format that's very common in CTFs. If the characters are all alphanumeric with the occasional `+`, `/`, and `=`, you're looking at Base64.

You could decode them all manually — or you could ask the AI assistant to look at the file and validate which one is legitimate. Pass it the full file path. It has a tool for checking this kind of thing, and it'll tell you which string is the real deal.

The real flag will be in the format `THM{...}`.

---

## What This Room Is Actually Teaching

In case it's not obvious by the end, the core theme here isn't just "do DFIR" — it's about what happens when an attacker targets an AI system specifically. The technique the attacker used to manipulate Oliver's AI assistant is called **prompt injection**, and it's genuinely becoming a real-world concern as companies start deploying internal LLM tools.

The attacker got the AI to do things it shouldn't have by crafting inputs designed to override its intended behaviour. Meanwhile, you turned around and used a *different* AI assistant to catch them. There's something satisfying about that.

The other thing worth noting: the attacker made a mistake. They left behind evidence of their own session in a packet capture that was still on the machine. In real incidents, attackers slip up — your job as an analyst is to find those slips before they're cleaned up.

---

Good luck. Take your time on the PCAP triage step especially — that's where most people either get it quickly or spin their wheels for a while.
