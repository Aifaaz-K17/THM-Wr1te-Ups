# TryHackMe — Cache Me Outside | Hint-Based Write-Up

**Difficulty:** Medium | **Category:** OSINT
**Room link:** https://tryhackme.com/room/cachemeoutside

*Same rules as always — try it yourself first. OSINT rooms especially have a way of teaching you things that reading a guide never quite does. Come back here when you're stuck, not before.*

---

## What's the Room About

You're tracking down a retired hacker who goes by the alias jiml33t. He's apparently tried to leave the scene and reinvent himself as an outdoors person — running, hiking, that kind of thing. The problem is, old habits die hard, and he's left traces of himself scattered all over the internet without realising it.

The room gives you a starting point — a screenshot of a conversation — and from there it's entirely up to you to follow the chain. No server to exploit, no binary to reverse. Just open sources and your ability to pivot from one piece of information to the next.

The name "Cache Me Outside" is doing double duty here. It's a meme reference obviously, but it's also a genuine hint at one of the techniques you'll need to use. Keep that in mind.

---

## Step 1 — The Starting Point

Look carefully at what the room gives you as its initial artifact. Don't just glance at it — study it. There's a link in there that most people spot quickly, and that link gets you to the first real profile you need to investigate.

Once you land on that profile, read everything. The bio, the activity, any linked accounts. Jim Lee — because that's who this is — has connected a few of his online presences together in a way that makes your job easier than he probably intended.

> **Stuck?** The first platform you land on is an outdoor activity app. It's not one of the mainstream social media giants, but it's popular in running and hiking communities. His profile there will point you directly to something else.

---

## Step 2 — GitHub and the Commit History

Once you find his GitHub, the obvious move is to browse the repository. Do that, but don't stop there.

Most people know that GitHub shows you code. Fewer people think about what else GitHub exposes. When someone makes a commit, Git records more than just the code change — it records the author's configured identity. And there's a way to view that raw data for any public commit.

> **Stuck?** Look into `.patch` files. GitHub exposes these for every commit, and they contain the full Git author metadata including an email address that doesn't always show up anywhere else. The URL format to access a patch file is straightforward — look at a commit URL and think about what you'd append to get the raw patch.

Once you have the email address, hold onto it. You'll use it more than once.

---

## Step 3 — Finding the Phone Number

This is the step that stumps most people, and it's honestly the cleverest part of the room.

You have an email address. You've probably already tried searching for it and come up somewhat empty. There are no obvious accounts tied to it on the major platforms. So how do you get a phone number from an email?

Think about what some people configure on their email accounts when they're not going to be checking it regularly. Something automatic. Something that replies without them having to be there.

> **Stuck?** Try sending an actual email to the address you found. Don't overthink the content — just send something. What comes back is the answer.

Pay attention to everything in the response, including anything that looks like it might be a signature or automated field. Hackers sometimes can't resist leaving little calling cards even in mundane things. There's a hex value in there worth noticing too, though it's more of an easter egg than a flag.

---

## Step 4 — Geolocation

At some point in your investigation you'll come across a photo posted to a social platform. It's a street photo — a road, some surroundings, nothing that immediately screams "this is where I live." But it contains enough to pin down a location if you look carefully.

Don't just reverse image search the whole photo — that probably won't help much here. Instead, look for text in the image. Signage, business names, anything readable. Even partial text can be searched.

> **Stuck?** There's a billboard visible in the image. The text on it references a real business. Search for that business name and see where it's located. Once you have a city, you can cross-reference with other details from the profile to confirm you're in the right place.

The country code on the phone number you found earlier should also give you a solid geographical anchor before you even look at the photo. Use that.

---

## Step 5 — The Hidden Feature

The outdoor activity platform from Step 1 has something built into it that's easy to miss. The room name is essentially pointing you toward it — something stored, something cached, something that isn't immediately visible on the surface.

Explore the profile more thoroughly than you did the first time. Look for anything interactive, any features that require input. If something asks for a password, think about what password Jim Lee would use given everything you now know about him.

> **Stuck?** Think about what information you've collected so far — username, name, other credentials. People reuse things. Also think laterally: the room name isn't just a meme. What does "cache" suggest technically?

---

## What This Room Gets Right

Cache Me Outside is a good demonstration of how OSINT investigations actually work in practice. You rarely find everything in one place. Instead you find one thing that points to another, which reveals something that unlocks a third. Each pivot depends on paying attention to details that most people scroll past.

The Git commit patch technique is genuinely useful and not widely known outside of security circles. Developers leak email addresses this way fairly regularly in real life, especially if they've set up their Git config with a personal or work email and never thought about the fact that it's baked into every commit they push to a public repo.

The auto-reply technique is a bit more social engineering flavoured — you're essentially probing an account to see if it's configured to reveal information automatically. It's low-tech and it works, which is sort of the point.

The room also does something subtle that I liked: it gives you a decoy. There's something on the outdoor platform that looks like it should matter but doesn't lead anywhere useful. Learning to recognise a dead end and back out of it rather than stubbornly pushing on is a real OSINT skill — probably more valuable than any individual technique.

---

Take notes as you go. Seriously. By the time you're mid-investigation you'll have usernames, emails, platform handles, a phone number, and a location all floating around. A scratchpad saves you from re-finding things you already found ten minutes ago.
